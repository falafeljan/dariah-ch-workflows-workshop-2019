\section*{Introduction}

\strut
\vspace{-4ex}

Research projects in the Digital Humanities (DH) continually establish new standards in digital workflows with novel tools. This development is facilitated by an increasing number of open-source projects, available for free use and maintained by a large community of voluntary contributors. Commonly respected guidelines for managing data in research projects, such as the [@fair] principles (Findable, Accessible, Interoperable, Reusable), establish a theoretical framework for these workflows, complementing technical architecture. Furthermore, by incorporating end-to-end, persistent references with technologies such as Digital Object Identifiers (DOIs), contemporary digital publishing takes on these frameworks. Thereby, references to particular versions of data can be resolved via open archives such as [@zenodo] and [@hal].

Reaching this level of quality in digital workflows is a major achievement for academia. Yet, the way we currently treat our data repositories is, in general, negligent. Often archived on platforms running on remote hardware in far-away data centers, people are rarely able to _exactly_ prove (that is, mathematically) _when_ and _what_ they contributed to a data repository. After all, at this point, digital data ownership is mostly given when data resides on one’s personal computing device. Local availability of data is itself advantageous: [@kleppmann2019] coined the term _local-first applications_ in reference to software that operates on locally stored data, as opposed to the popular approach of _thin clients_, where data is mainly pushed to servers running remotely. However, local-first applications further question the necessity of centralized services for real-time collaboration—take Google Docs—by asserting that even as data leaves one’s devices, digital ownership can be proven by cryptographic means. This concept provides one major takeaway: personal data doesn’t necessarily need to be shared with third parties when collaborating with peers.

Applying this concept to research, we propose a distinction between personal and institutional data in the context of annotation. Artifacts belonging to the institutional domain, such as classic texts or digitized manuscripts, are stored remotely. Annotations on these sources, however, can be stored on an individual’s device. Our work describes such workflows and, by introducing a system called Hyperwell, provides an architecture that leverages contemporary peer-to-peer technology to realize local-first, distributed, and collaborative annotation environments.

## Collaboration in the digital humanities

In the wake of Web 2.0—a technological development that emerged after the dot-com bubble burst in 2001—the internet became more open and accessible to the general public. Collaboration in research and particularly in DH adopted this trend, according to  [@davidson2008], while the web tended towards the social sharing of resources on websites. Two advancements then materialized within DH: as human expression became increasingly digital, the humanities’ workflows turned digital, too; subsequently, information on the past has been digitized, emphasizing digital practice within the humanities.

### Exposing history

The FAIR principles consist of four imperatives for digital workflows—Findability, Accessibility, Interoperability, and Reusability—and have been rapidly adopted among scholars. Some best practices go even further by explicitly recommending version control and the recording of additional metadata, such as [@nowogrodzki2020]. Maintaining a log of changes is a convenient, self-documenting step in end-to-end digital workflows.

Over the years, the [@git] version-control system has been established as a popular tool in software development, as it allows users to write code in a change-based workflow. Collections of changes are bundled into a commit, which is then written into an immutable log and distributed to others. [@kreps2013] states that this append-only log makes it straightforward for log-based databases to maintain a persistent history of changes and enables time-traveling between past states.

### Web annotation

With pen-and-paper annotation, one’s expression is basically unlimited: lines, highlights, and words can connect any visible artifact. Transforming such free interaction into digital processes can entail an unforeseeable complexity. However, as [@marshall1997] observed while analyzing a collection of students’ used textbooks, a majority of their annotations fit into a categorization of six distinct schemes, varying in their focus and level of detail from simple marginal symbols up to complex sidenotes.

Published by the World Wide Web Consortium (W3C), the Web Annotation specification by [@sanderson2013] is built upon an ontology that is expected to be as versatile as possible, covering annotation schemes such as the above by providing varieties of target selection mechanisms and content types. The fundamental components of an annotation within this ontology are its target (a web resource) and its body (an entity). By using semantic expressions, an annotation body can convey complex structures, like their own motivation (for example, editing a passage) and their relations to other objects (for example, referring to a particular person). These structures could meet the semantic requirements of digital datasets in the humanities, such as digital gazetteers.

## Personal annotations with Hyperwell

With our work on personal annotation, Hyperwell, we aim to address several concerns at once. Hyperwell imposes a clear architectural distinction between _personal_ and _institutional_ work enabled by leveraging peer-to-peer technology. We introduce the notion of a digital, personal notebook, residing on individuals’ devices. Such a notebook is a collection of annotations on a single resource and complies with the [@web-anno-data-model].

\begin{figure}
  \includegraphics[width=\textwidth]{figures/architecture}
  \caption{The Hyperwell architecture. Peers exchange their notebooks in real-time (1). Gateways, run by institutions, archive selected notebooks and bridge them into the web (2). Web applications can access annotations via gateways, as they implement the Web Annotation protocol (3). These applications can load canonical resources via services such as CTS or IIIF (4).}
  \label{fig:architecture}
\end{figure}

Figure~\ref{fig:architecture} outlines the architecture of Hyperwell. Each notebook can be shared directly with selected peers. By exposing an immutable, append-only log of all changes made to it, each version of a notebook can be referenced individually and facilitates archiving. Special requirements on the data types used allow the realization of real-time collaboration without the need for a central authority to resolve merge conflicts between multiple peers. Finally, end-to-end referencing of such workflows becomes possible, as each version of a notebook can target canonical resources, such as passages via Canonical Text Services (CTS) or multimedia resources via [@iiif].

### Bridging the gap with gateways

Traditional notions of _pure_ P2P networks impose the requirement that within such networks, resources are shared by nodes homogeneously, as [@schollmeier2002] notes. This homogeneity ensures that data within these networks is genuinely decentralized. System architects occasionally break with this homogeneity for various reasons; for instance, to improve performance or to ensure interoperability with other networks.

In a patent, [@matsubara2010] sketch how such interoperability could be realized by describing a gateway between a peer-to-peer network and the web. Similar to the gateway pictured in Figure 1, it acts as an intermediary between individual peers and requests from web clients. [@kassel2020] implements a gateway for the Hyperwell architecture that acts both as a passive peer within the peer-to-peer network and as a server for web clients. The gateway implements the [@web-anno-protocol] for compliance with environments using the Web Annotation specification.

### Institutional archival of notebooks

Along with the aforementioned advantages of peer-to-peer networks, there is also an associated risk: if the device serving a certain resource is disconnected from the network, this resource is not available to other peers. In an academic context, however, and especially for published datasets or collaborative work, continuous data availability is crucial.

Supporting nodes can improve data availability and, hence, the overall quality of a peer-to-peer network. By _pinning_ or _seeding_ resources, such nodes can mirror other peers’ data without actually causing any increase in the centralization of resources; on the contrary, this affects a further distribution. Furthermore, as volatile infrastructure, supporting nodes maintain original ownership. Seeding became an integral part of BitTorrent systems, as @legout2007 have noted, while incentive mechanisms can further help to maintain supporting infrastructures. Within the architecture of Hyperwell, such a supporting infrastructure operates in the interest of institutions: they can ensure data availability for affiliated researchers as well as archive repositories in their entirety, as each repository contains its complete history.

### Real-time collaboration

Merging changes from different sources is rarely a trivial task, especially within a distributed environment. Collaborative applications like Google Docs and Trello use a central authority—their servers—to solve these conflicts, but this requires a continuous internet connection from clients and exclusively relies on this authority. However, contemporary technology can already address this challenge: Conflict-Free Replicated Data Types (CRDTs) impose several theoretical merging strategies on data in order to obtain consistent and fail-safe merging in distributed networks, which [@kleppmann2019] leverage for decentralized collaboration “in spite of the cloud”.

To realize this functionality in Hyperwell, we have utilized [@hypermerge], a library that combines several technologies of distributed computing for realizing real-time, peer-to-peer collaboration:

* [@automerge], a JavaScript-based CRDT implementation,
* [@hypercore], a distributed append-only log, allowing us to immutably store and distribute changes on a dataset, and
* [@hyperswarm], a stack of distributed networking technologies for establishing connections between peers without centralized discovery.

Both hypercore and hyperswarm are being actively developed by the Dat Protocol foundation. This not-for-profit organization builds the Dat data-sharing protocol, introduced by [@robinson2018], for use in research and civic technology.

## Outlook

With Hyperwell, we have produced a collaborative, peer-to-peer annotation system that builds upon contemporary peer-to-peer technology and implements the Web Annotation specification. Hyperwell aims to address issues concerning data privacy and digital sovereignty in DH research, facilitated by centralized platforms. Establishing a separation of personal and institutional data, we present a gateway service for Hyperwell, bridging personal, distributed annotation notebooks and the web for interoperability with existing annotation environments.

A forthcoming Master’s thesis by Jan Kaßel at Universität Leipzig includes further work that will focus on evaluating the presented architecture and its entailing collaborative workflows. To provide a necessary prototype environment, we aim to build two applications: First, a local-first notebook application that will manage annotations by storing them locally as well as indexing them for local search. Second, for conducting actual usability and workflow evaluation, a proof-of-concept collaborative environment that integrates canonical resources, such as CTS passages or multimedia IIIF manifests.
