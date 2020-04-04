## Introduction

\strut
\vspace{-4ex}

Research projects in the Digital Humanities continuously establish new standards in digital workflows with novel tools. This development is facilitated by an increasing number of open source projects, available for free use and maintained by a large community of voluntary contributors. Commonly respected principles for managing data in research projects, such as the FAIR\footnote{\url{https://www.go-fair.org/fair-principles/}} principles (Findable, Accessible, Interoperable, Reusable), establish a theoretical framework for these workflows, complementing technical architecture. Furthermore, by incorporating end-to-end, persistent references with technologies such as Digital Object Identifiers (DOIs), contemporary digital publishing takes on these frameworks. Thereby, references to particular versions of data can be resolved via open archives such as Zenodo\footnote{\url{https://zenodo.org/}} and HAL\footnote{\url{https://hal.archives-ouvertes.fr/}}.

Reaching this level of quality in digital workflows is a major achievement for academia. Yet, the way we currently treat our data repositories is, in general, negligent. Often archived on platforms running on remote hardware in far-away data centers, people are rarely able to _exactly_ prove (that is, mathematically) _when_ and _what_ they contributed to a data repository. After all, at this point, digital data ownership is mostly given when data resides on one’s personal computing device. Local availability of data is itself advantageous: In \citeyear{kleppmann2019}, \citeauthor*{kleppmann2019} coined the term _local-first applications_ in reference to software that operates on locally stored data, as opposed to the popular approach of _thin clients_, where data is mainly pushed into servers running remotely. However, local-first applications further question the necessity of centralized services for real-time collaboration—take Google Docs—by asserting that even as data leaves one’s devices, digital ownership can be proven by cryptographic means. This concept provides one major takeaway: Personal data doesn’t necessarily need to be shared with third parties when collaborating with peers.

Applying this concept to research, we aim to pose a distinction between personal and institutional data in the context of annotation: Artifacts, such as classic texts or digitized manuscripts, belonging into the institutional domain, are being stored remotely. Annotations on these sources, however, can be stored on an individual’s device. Our work describes such workflows and, by introducing a system called Hyperwell, provides an architecture that leverages contemporary peer-to-peer technology to realize local-first, distributed, and collaborative annotation environments.


## Collaboration in the Digital Humanities

In the wake of _Web 2.0_—a technological development that emerged after the dot-com bubble burst in 2001—the internet became more open and accessible to the general public. Collaboration in research, and particularly in the Digital Humanities, adopted this trend, as the web tended towards the social sharing of resources on websites \parencite{davidson2008}. Two advancements then materialized within the Digital Humanities: as human expression became increasingly digital, Humanities’ workflows turned digital, too; subsequently, information on the past has been digitized, emphasizing digital practice within the Humanities.

### Exposing History

The FAIR principles consist of four imperatives for digital workflows—Findability, Accessibility, Interoperability, and Reusability—, and have been rapidly adopted among scholars. Some best practices continue to go even further by explicitly recommending version control and the recording of additional metadata \parencite{nowogrodzki2020}. Maintaining a log of changes is a convenient, self-documenting step in end-to-end digital workflows.

Over the years, the Git\footnote{\url{https://git-scm.com/}} version control system has been established as a popular tool in software development, as it allows users to write code in a change-based workflow: Collections of changes are bundled into a commit, which again is written into an immutable log and then distributed to others. This log, also called an append-only log, makes it straightforward to maintain a persistent history of changes and enables time-traveling among past states \parencite{kreps2013}.

### Web Annotation

With pen-and-paper annotation, one’s expression is basically unlimited: lines, highlightings, and words can connect any visible artifact. Transforming such free interaction into digital processes can entail an unforeseeable complexity. However, as \citeauthor{marshall1997} noted while analyzing a collection of used students’ textbooks, a majority of their annotations fit into a categorization of six distinct schemes, varying in their focus and level of detail from simple marginal symbols up to complex sidenotes \parencite{marshall1997}.

Published by the World Wide Web Consortium (W3C), the Web Annotation specification is built upon an ontology that is expected to be as versatile as possible, covering annotation schemes such as the above by providing varieties of target selection mechanisms and content types \parencite{sanderson2013}. The fundamental parts of an annotation within this ontology are its target (a web resource) and its body (an entity). By using semantic expressions, an annotation body can convey complex structures, such as their own motivation (for example, editing a passage) and their relations to other objects (for example, referring to a particular person). Such structures could meet the semantic requirements of digital datasets in the Humanities, such as gazetteers in the Classics. 


## Personal Annotations with Hyperwell

With our work on personal annotation, Hyperwell, we aim to address several concerns at once. Hyperwell imposes a clear architectural distinction between _personal_ and _institutional_ work enabled by leveraging peer-to-peer technology. We introduce the notion of a digital, personal notebook, residing on individuals’ devices. Such a notebook is a collection of annotations on a single resource and complies with the Web Annotation data model\footnote{\url{https://www.w3.org/TR/annotation-model/}}.

\begin{figure}
  \includegraphics[width=\textwidth]{figures/architecture}
  \caption{The Hyperwell architecture. Peers exchange their notebooks in real-time (1). Gateways, run by institutions, archive selected notebooks and bridge them into the web (2). Web applications can access annotations via gateways, as they implement the Web Annotation protocol (3). These applications can load canonical resources via services such as CTS or IIIF (4).}
  \label{fig/architecture}
\end{figure}

Figure~\ref{fig/architecture} outlines the architecture of Hyperwell. Each notebook can be shared directly with selected peers. By exposing an immutable, append-only log of all changes made to it, each version of a notebook can be referenced individually and facilitates archiving. Special requirements on the data types used allow the realization of real-time collaboration without the need for a central authority to solve merge conflicts between multiple peers. Finally, end-to-end referencing of such workflows becomes possible, as each version of a notebook can target canonical resources, such as passages via Canonical Text Services (CTS) or multimedia resources via IIIF\footnote{\url{https://iiif.io/}}.

### Bridging the Gap with Gateways

Classic notions of _pure_ P2P networks impose the limitation that within such networks, resources are shared by nodes homogeneously, as \textcite{schollmeier2002} notes. This homogeneity ensures that data within these networks is genuinely decentralized. Network architects occasionally break with this homogeneity for various reasons, for instance, to improve performance or to ensure interoperability with other networks.

In a patent from \citeyear{matsubara2010}, \citeauthor{matsubara2010} sketch how such interoperability could be realized by describing a gateway between a peer-to-peer network and the web. Similar to the gateway pictured in Figure~\ref{fig/architecture}, it acts as an intermediary between individual peers and requests from web clients. We implemented a gateway for Hyperwell that acts both as a passive peer within the peer-to-peer network and as a server for web clients \parencite{kassel2020}. The gateway implements the Web Annotation protocol\footnote{\url{https://www.w3.org/TR/annotation-protocol/}} for compliance with environments using the Web Annotation specification.

### Institutional Archival of Notebooks

Along with the aforementioned advantageous prospects of peer-to-peer networks, there is also a particular risk: If the device serving a certain resource is disconnected from the network, this resource is not available to other peers. In the academic context, however, and especially for published datasets or collaborative work, continuous data availability is crucial.

Supporting nodes can improve data availability and, hence, the overall quality of a peer-to-peer network. By _pinning_ or _seeding_ resources, such nodes can mirror other peers’ data without actually causing any increase in the centralization of resources—quite the contrary, this affects a further distribution, while as volatile infrastructure, supporting nodes maintain original ownership \parencite{benet2014,legout2007}. Within the architecture of Hyperwell, such a supporting infrastructure operates in the interest of institutions: They can not only ensure data availability for affiliated researchers, but also archive repositories in their entirety, as each repository contains its complete history. 

### Real-Time Collaboration

Merging changes from different sources is rarely a trivial task, especially within a distributed environment. Collaborative applications like Google Docs and Trello use a central authority—their servers—to solve these conflicts, but this requires a continuous internet connection from clients and relies on this authority. However, contemporary technology can already address this challenge: Conflict-Free Replicated Data Types (CRDTs) impose several theoretical merging strategies on data in order to obtain consistent and fail-safe merging in distributed networks \parencite{kleppmann2019}.

To realize this functionality in Hyperwell, we utilize _hypermerge_\footnote{\url{https://github.com/automerge/hypermerge}}, a library that combines several distributed technologies for realizing real-time, peer-to-peer collaboration:

* _automerge_\footnote{\url{https://github.com/automerge/automerge}}, a JavaScript-based CRDT implementation,
* _hypercore_\footnote{\url{https://github.com/mafintosh/hypercore}}, a distributed append-only log, allowing us to immutably store and distribute changes on a dataset, and
* _hyperswarm_\footnote{\url{https://github.com/hyperswarm/hyperswarm}}, a stack of distributed networking technologies for establishing connections between peers without centralized discovery.

Both hypercore and hyperswarm are being actively developed by the Dat Protocol project, a non-profit group building a distributed data-sharing protocol \parencite{robinson2018}.


## Outlook

With Hyperwell, we presented a collaborative, peer-to-peer annotation system that builds upon contemporary peer-to-peer technology and implements the Web Annotation specification. Hyperwell aims to address issues concerning data privacy and digital sovereignty in Digital Humanities research, facilitated by centralized platforms. Establishing a separation of personal and institutional data, we present a gateway service for Hyperwell, bridging personal, distributed annotation notebooks into the web for interoperability with existing annotation environments.

Further work will focus on evaluating the presented architecture and its entailing collaborative workflows. To provide the necessary prototype application for such an environment, we aim to build two applications: First, a local-first notebook application that will manage annotations by storing them locally and indexing them for local search. Second—for conducting actual usability and workflow evaluation—a proof-of-concept, collaborative environment that integrates canonical resources such as CTS passages or multimedia IIIF manifests.
