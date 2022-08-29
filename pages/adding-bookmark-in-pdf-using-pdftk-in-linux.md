refer [[Shell Tools and scriptting]]


# Adding bookmarks in pdf
First we need `pdftk` package in linux 

* Create a shell script file ``pdftk_installer.sh`` with the following content. 
```bash
    #!/bin/bash
    #
    # author: abu
    # date:   July 3 2019 (ver. 1.1)
    # description: bash script to install pdftk on Ubuntu 18.04 for amd64 machines
    ##############################################################################
    #
    # change to /tmp directory
    cd /tmp
    # download packages
    wget http://launchpadlibrarian.net/340410966/libgcj17_6.4.0-8ubuntu1_amd64.deb \
    http://launchpadlibrarian.net/337429932/libgcj-common_6.4-3ubuntu1_all.deb \
    https://launchpad.net/ubuntu/+source/pdftk/2.02-4build1/+build/10581759/+files/pdftk_2.02-4build1_amd64.deb \
    https://launchpad.net/ubuntu/+source/pdftk/2.02-4build1/+build/10581759/+files/pdftk-dbg_2.02-4build1_amd64.deb

    echo -e "Packages for pdftk downloaded\n\n"
    # install packages
    echo -e "\n\n Installing pdftk: \n\n"
    sudo apt-get install ./libgcj17_6.4.0-8ubuntu1_amd64.deb \
        ./libgcj-common_6.4-3ubuntu1_all.deb \
        ./pdftk_2.02-4build1_amd64.deb \
        ./pdftk-dbg_2.02-4build1_amd64.deb
    echo -e "\n\n pdftk installed\n"
    echo -e "   try it in shell with: > pdftk \n"
    # delete deb files in /tmp directory
    rm ./libgcj17_6.4.0-8ubuntu1_amd64.deb
    rm ./libgcj-common_6.4-3ubuntu1_all.deb
    rm ./pdftk_2.02-4build1_amd64.deb
    rm ./pdftk-dbg_2.02-4build1_amd64.deb
```

* Run the shell script. This will install pdftk on your linux machine
	```shell
	./pdftk_installer.sh
	```

* Create a bookmark reference file to be updated as the metadata of the pdf. This illustration is for inserting the bookmark metadata on the following pdf. Assuming this is saved as `5G_NR_book.pdf` 

![[Dahlman et al. - 2021 - 5G NR the next generation wireless access technol.pdf]]


* Save this to a `.txt` file for e.g. ``bookmark.txt`` . (This example sample bookmark data is only corrosponds to the above pdf in the example). The entire `bookmark.txt` is given following this example. 

```text
BookmarkBegin
BookmarkTitle: CHAPTER 14: Scheduling
BookmarkLevel: 1
BookmarkPageNumber: 307
BookmarkBegin
BookmarkTitle: 14.1 Dynamic Downlink Scheduling
BookmarkLevel: 2
BookmarkPageNumber: 307
BookmarkBegin
BookmarkTitle: 14.1.1 Downlink Preemption Handling
BookmarkLevel: 3
BookmarkPageNumber: 310
BookmarkBegin
BookmarkTitle: 14.2 Dynamic Uplink Scheduling
BookmarkLevel: 2
BookmarkPageNumber: 311
BookmarkBegin
BookmarkTitle: 14.2.1 Uplink Priority Handling and Logical-Channel Multiplexing
BookmarkLevel: 3
BookmarkPageNumber: 314
BookmarkBegin
BookmarkTitle: 14.2.2 Scheduling Request
BookmarkLevel: 3
BookmarkPageNumber: 316
BookmarkBegin
BookmarkTitle: 14.2.3 Buffer-Status Reports
BookmarkLevel: 3
BookmarkPageNumber: 319
BookmarkBegin
BookmarkTitle: 14.2.4 Power Headroom Reports
BookmarkLevel: 3
BookmarkPageNumber: 320
```

[bookmark.txt](../docs/bookmark.txt)

* Finally, update the `.pdf` file with the bookmark metadata. `5G_NR_book_Bkmrk_added.pdf` is the output file with the bookmark metadata added.

```
pdftk 5G_NR_book.pdf update_info bookmark.txt output 5G_NR_book_Bkmrk_added.pdf
```
