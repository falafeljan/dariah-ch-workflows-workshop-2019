# From Me to You: Peer-to-Peer Collaboration with Linked Data

[![DOI](https://zenodo.org/badge/206756297.svg)](https://zenodo.org/badge/latestdoi/206756297)

Extended abstract, presentation slides, and proceedings paper of our ([Dr. Thomas Koentges](http://thomaskoentges.io/) and [Jan Kaßel](https://kassel.works/)) contribution to the 2nd [DARIAH-CH workshop](https://dariah-ch-ws19.sciencesconf.org/resource/page/id/2), “Sharing the Experience: Workflows for the Digital Humanities”, December 5-6, 2019, in Neuchâtel, Switzerland. 

Abstract of the proceedings paper:
> In recent years, Digital Humanities’ collaborative nature caused an awakening of digitally native research practice, where interdisciplinary workflows commonly feed into centralized data repositories. Connecting these repositories, the W3C’s Web Annotation specification builds upon Linked Data principles for targeting any web resource or Linked Data entity with syntactic and semantic annotation. However, today’s platform-centric infrastructure diminishes the distinction between institutions’ and individuals’ data. This poses issues of digital ownership, interoperability, and privacy of data stored on centralized services. With Hyperwell, we aim to address these issues by introducing a novel architecture that offers real-time, distributed synchronization of Web Annotations, leveraging contemporary peer-to-peer technology. Extending the peer-to-peer network, institutions provide Hyperwell gateways that bridge peers’ annotations into the web. These gateways affirm a researcher’s affiliation while acting as a mere mirror of researchers’ data and maintaining digital ownership.

### Proceedings Paper

Make sure to have LaTeX and `latexmk` installed (`sudo tlmgr install latexmk`). Then simply run `(cd paper; make)` to build the paper PDF. We will invoke `pdflatex` with the `--shell-escape` flag, as this is required for building from the Markdown source.

The raw contents of the paper are located in [`paper/paper.md`](paper/paper.md).

### License

This work is licensed under a Creative Commons [Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

