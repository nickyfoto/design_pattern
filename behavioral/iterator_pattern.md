


```java

import java.util.Iterator;

public class StockIterator implements Iterator {

  private Inventory inventory;
  private int index = 0;

  public StockIterator(Inventory inventory) {
    this.inventory = inventory;

  }

  public boolean hasNext() {
    Item[] items = inventory.getItems();
    if (index < items.length) {
      return true;
    } else {
      return false;
    }
  }

  public Item next() {
    Item[] items = inventory.getItems();
    if (hasNext()) {
      Item item = items[index++];
      if (item.getQuantity() > 0) {
        return item;
      } else {
        return next();
      }
    } else {
      return null;
    }
  }

  public void remove() {

  }

}


public class Inventory implements Iterable {

  private Item[] items;

  public Inventory(Item... items) {
    this.items = items;
  }

  public Item[] getItems() {
    return items;
  }

  public StockIterator iterator() {
    return new StockIterator(this);
  }

}


public class Item {

  String name;
  int quantity;

  public Item(String name, int quantity) {
    this.name = name;
    this.quantity = quantity;
  }

  public String getName() {
    return name;
  }

  public int getQuantity() {
    return quantity;
  }

}

public class Main {

  public static void main(String[] args) {

    Item pens = new Item("pens", 175);
    Item pencils = new Item("pencils", 0);
    Item paper = new Item("paper", 500);

    Inventory inventory = new Inventory(pens, pencils, paper);
    StockIterator iterator = inventory.iterator();
    while (iterator.hasNext()) {
      Item item = iterator.next();
      System.out.println(item.getName());
    }


  }

}

```