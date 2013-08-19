DOT Printers
============

#### Source code for all languages will be released in the near future.   
  
Simple helpers for generating [Graphviz](http://www.graphviz.org/) DOT files in various programming languages.  
Currently includes generators for C, C++, Java, Python and C#.
  
The generators are very simple, definining a series of shapes and colors and two main functions: *create shape* and *link two shapes*. The shape type, label and color can be customized, while for the link the color, line width, pattern and label can be customized.  
  
#### Example of printing a [Trie](http://en.wikipedia.org/wiki/Trie) in Java.

```
// Basic definition for the Trie class.
class Trie {
    boolean isTerminator;
    Map<Character, Trie> children;
    
    private void printToDOT(DotPrinter printer) {
        // Create a shape for the current node.
        DotPrinter.Color shapeColor = isTerminator ? DotPrinter.Color.Red : 
                                                     DotPrinter.Color.Blue;
        printer.createNode(this, "", DotPrinter.Shape.Circle, shapeColor);
        
        // Recursively create shapes for all child nodes  
        // and link them to the current shape.
        for(Map.Entry<Character, Trie> entry : children.entrySet()) {
            entry.getValue().printToDOT(printer);
            printer.createLink(this, entry.getValue(), String.valueOf(entry.getKey()));
        }
    }
    
    public void printToDOT(BufferedWriter writer) {
        // Create a DOT printer and create shapes for the subtree.
        DotPrinter printer = new DotPrinter(writer);
        printer.beginGraph();
        printToDOT(printer);
        printer.endGraph();
    }
}
```  

A good, cross-platform viewer for DOT files is [ZGRView](http://zvtm.sourceforge.net/zgrviewer.html) - it requires the [JRE](http://www.oracle.com/technetwork/java/javase/downloads/index.html) to be installed.
