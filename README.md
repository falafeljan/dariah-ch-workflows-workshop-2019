# From Me to You: Peer-to-Peer Collaboration With Linked Data

Abstract, presentation slides, and proceedings paper for our ([Dr. Thomas Koentges](http://thomaskoentges.io/) and Jan Kaßel) contribution to the 2nd [DARIAH-CH workshop](https://dariah-ch-ws19.sciencesconf.org/resource/page/id/2), "Sharing the Experience: Workflows for the Digital Humanities", December 5-6, 2019, in Neuchâtel, Switzerland. 

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

Also, make sure to have `latexmk` installed (`sudo tlmgr install latexmk`). Then simply run `./build.sh` from within the `paper` folder to build the paper PDF. We will invoke `pdflatex` with the `--shell-escape` flag, as this is required for building from the Markdown source.

The contents of the paper are located in `paper/paper.md`.
