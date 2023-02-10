Useful, but somewhat crude spripts for syncing the datasets across the various nodes
in our DGX cluster. 

WARNING these scripts make quite a few assumptions... and need to be used with some caution.

use scp to copy files... all these scripts will overwirte whatever is in the target

   a-scp           copies all the files in all the sub-diretories under /raid/parquet_sf3000 
                   form the local node to the target node specified (by node number)

   scp-all         a more parametized version a-scp (accpet dataset parameter). has not
                   been tested very much - could be buggy

   p-scp           similar to a-scp, but copies the sub-directories in parallel and binds
                   to the high-speed nic... this was buggy early on (issues with network setup)
                   so it was not used (much)... may work now but an additional word of caution.


these use rysyn instead of scp ... generally slower but if if you have partial copies they are 
much more friendly (the will not overwrite what is already copied  and in that case can be faster).


   rsync-small    just does the smaller datasets ... this one does not take long at all

   rsync-medium   similar but does the medium sized datasets... can easily be done in parallel with 
                  rsync-small

   rsync-big      does on big dastset at a time (you pass it store_sales, catalog_sales, or web_sales)



Verification

   verfy          used to collect up "contents_dataset_node" files that can be diffed to veify 
                  the contents of on all nodes

