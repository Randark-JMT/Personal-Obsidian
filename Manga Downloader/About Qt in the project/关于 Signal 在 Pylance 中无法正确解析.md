一个很重要的Stackoverflow文章： [How to properly setup vscode with pyside? Missing suggestions](https://stackoverflow.com/questions/67519583/how-to-properly-setup-vscode-with-pyside-missing-suggestions)
题主所使用的版本为`Pyside2`，但是其实在`Pyside2`和`Pyside6`中，均有出现这个问题。这个问题在网友分析之后，发现是由于`Pylance`无法正确识别`Pyside`中的信号对象为`object`所导致的。
