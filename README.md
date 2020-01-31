# From Me to You: Peer-to-Peer Collaboration With Linked Data

[![DOI](https://zenodo.org/badge/206756297.svg)](https://zenodo.org/badge/latestdoi/206756297)

Abstract, presentation slides, and proceedings paper for our ([Dr. Thomas Koentges](http://thomaskoentges.io/) and Jan Kaßel) contribution to the 2nd [DARIAH-CH workshop](https://dariah-ch-ws19.sciencesconf.org/resource/page/id/2), "Sharing the Experience: Workflows for the Digital Humanities", December 5-6, 2019, in Neuchâtel, Switzerland. 

Abstract of the proceedings paper:
> In recent years, Digital Humanities' collaborative nature caused a wake digitally-native research practice, where interdisciplinary workflows commonly feed into centralized data repositories. Connecting these repositories, the W3C’s Web Annotation specification builds upon Linked Data principles for targeting any Web resource or Linked Data entity with syntactic and semantic annotation. However, today’s platform-centric infrastructure diminishes the distinction between institutional and individuals’ data. This poses issues of digital ownership, interoperability, and privacy of data stored on centralized services. With Hyperwell, we aim to address these issues by introducing a novel architecture that offers real-time, distributed synchronization of Web Annotations, leveraging contemporary peer-to-peer technology. Extending the peer-to-peer network, institutions provide Hyperwell gateways that bridge peers’ annotations into the common web. These gateways affirm a researcher’s affiliation while acting as a mere mirror of researchers’ data and maintaining digital ownership.

### Proceedings Paper

In order to build the paper via LaTeX (likely if using Basic TeX) you'll need to install the following packages:

```bash
sudo tlmgr install \
  preprint titlesec subfigure \
  enumitem pgfplots courier \
  csvsimple gobble paralist \
  biber biblatex biblatex-apa \
  markdown
```

Also, make sure to have `latexmk` installed (`sudo tlmgr install latexmk`). Then simply run `(cd paper; ./build.sh)` to build the paper PDF. We will invoke `pdflatex` with the `--shell-escape` flag, as this is required for building from the Markdown source.

The contents of the paper are located in [`paper/paper.md`](paper/paper.md).
