# java-simple-quadtree
A quadtree written in Java. Supports insert, update, search, remove, and more! Plenty of unit tests and also a performance report to compare with a brute force method.

Import as a Gradle project, and run the jar command to produce the .jar (or used the one checked in).

## Creating the QuadTree and inserting items
```java

/**
* Default quadTree is 100 * 100, will store a maximum of 10 objects per node, and will grow to a depth of 5.
*/

QuadTree quadTree = new QuadTree();

/**
* Insert some items that implement the RectangleObject interface.
* For demonstration, the SearchRectangleObject implementation of the RectangleObject interface is used,
* however you can easily implement the interface and insert your own objects.
*/

quadTree.insert(new SearchRectangleObject(5.0, 5.0, 10.0, 10.0));
quadTree.insert(new SearchRectangleObject(25.0, 25.0, 10.0, 10.0));
quadTree.insert(new SearchRectangleObject(5.0, 5.0, 12.0, 10.0));
quadTree.insert(new SearchRectangleObject(25.0, 25.0, 10.0, 10.0));
quadTree.insert(new SearchRectangleObject(5.0, 25.0, 20.0, 10.0));
quadTree.insert(new SearchRectangleObject(25.0, 5.0, 10.0, 10.0));

```
## Querying the QuadTree

```java

/**
* The QuadTree can be easily queried using the search method. Pass in a SearchRectangleObject with
* the bounds you want to search. It will return the RectangleObjects that overlap with 
* your SearchRectangleObject.
*
* The following quereis the 100 * 100 area with the top-left corner at x = 0, y = 0
*/

List<RectangleObject> objects = quadTree.search(new SearchRectangleObject(0.0, 0.0, 100.0, 100.0));

```

## Updating items in the QuadTree
```java

/**
* In order for an items position in the QuadTree to be updated, it must be given an Id when it is inserted.
*/

quadTree.insert(new SearchRectangleObject(0.0, 0.0, 10.0, 10.0, "1"));

/**
* Note that you need to provide the coordinates of a rectangle object to move it. If only an Id were
* required then the entire tree would need to be traversed to find the object. In this example, 
* the item location is updated to x = 5.0, y = 5.0. 
* Updating an object will only change the x, y, width, and height properties of that object.
*/

quadTree.update(new SearchRectangleObject(0.0, 0.0, 10.0, 10.0, "1"), 
      new SearchRectangleObject(5.0, 5.0, 10.0, 10.0));

```
## Removing an item from the QuadTree
```java

/**
* Returns the removed object from the QuadTree, note that this method does not currently cause any 
* rebalancing of nodes. You must provide the coordinates of the objecct to remove, as well as the id.
*/
RectangleObject object = quadTree.remove(new SearchRectangleObject(0.0, 0.0, 5.0, 5.0, "1"));

```

## Miscellaneous QuadTree methods
```java

//Return the depth of the QuadTree, it will at least be 1 for the root node
quadTree.getDepth();

//Get the total number of objects in the QuadTree
quadTree.getTotalObjects();

//Remove all objects from the QuadTree
quadTree.clear();

```