#Triejs
A Javascript implementation of a trie data structure with an extensible data 
model to easily customize to any need.

##Usage

###Basic
Creating a trie is as easy as creating a new object:

    > var trie = new exports.Triejs();

To add a word with some data associated it call `addWord`:

    > trie.addWord(<word>, <data>);

Now given any prefix of letters, you can return results possible words using `getPrefix`:

    > trie.getPrefix(<word>);
      => <data>

###Advanced

To customize the data just pass optional data, including functions to support data manipulation.  These 
include `sort` to sort data being entered, `insert` to customize how data is input, `copy` for moving data 
between nodes in the trie, and `clip` for removing data from the cache layer if it grows too big.

####Example

Options are passed via the constructor as a hash like so:

    var trie = new exports.Triejs({
      // sort the data in the context 'this'
      sort: function() {
        this.sort(function(a, b) {
          return b.rank - a.rank;
        });
      }
      // insert data into the target
      , insert: function(target, data) {
        // override for non array implementation
      }
      // clip the data in the context 'this' to length max
      , clip: function(max) {
        this.splice(0, this.length - max);
      }
      // return a copy of data
      , copy: function(data) {
        // override and return new data for non array implementation
      }
    });
