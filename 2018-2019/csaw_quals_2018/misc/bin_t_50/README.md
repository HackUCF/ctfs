# bin_t

## Information

*CTF*: CSAW Quals 2018

*Category*: Misc

*Point Value*: 50

*Writeup Author*: github.com/nalshihabi


This challenge was pretty straightforward, given nodes, insert them into an AVL tree and the output the preorder traversal. I did not feel like writing up my own AVL tree so I went and found some code for it:

https://gist.github.com/girish3/a8e3931154af4da89995


I made changes to the main function so that I can just copy-paste input/output  and I created a preorder traversal function by slightly modifying the inorder_traversal function already present.

Changes to main function:
```Python
if __name__ == "__main__": 
    a = AVLTree()
    print "----- Inserting -------"
    inlist = [int(_) for _ in raw_input("input string: ").strip().split(',')]
    for i in inlist: 
        a.insert(i)
         
    a.display()
    
    print()
    print ",".join([str(_) for _ in a.preorder_traversal()])
```

Preorder Traversal function:
```Python
def preorder_traversal(self):
    if self.node == None:
        return [] 
    
    inlist = [] 

    inlist.append(self.node.key)

    l = self.node.left.preorder_traversal()
    for i in l: 
        inlist.append(i) 

    l = self.node.right.preorder_traversal()
    for i in l: 
        inlist.append(i) 

    return inlist 
```

Once these changes were made, I connected to the challenge and copy-pasted the input from the challenge into my script and then copy-pasted the output from the script into the challenge and got the flag:
```
flag{HOW_WAS_IT_NAVIGATING_THAT_FOREST?}
```
