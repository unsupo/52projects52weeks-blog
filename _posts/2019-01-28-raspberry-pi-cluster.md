---
ID: 159
post_title: Raspberry Pi Cluster
author: jarndt
post_excerpt: ""
layout: post
permalink: >
  https://52projects52weeks.com/2019/01/28/raspberry-pi-cluster/
published: true
post_date: 2019-01-28 03:41:32
---
<!-- wp:heading -->

## Motivation

<!-- /wp:heading -->

<!-- wp:paragraph -->

Clusters are very useful in a number of use cases. I will be using a cluster for 3 main purposes. First use case is to learn about how computing clusters work and function. Second is for redundant servers and resilient microservices. Finally they are very useful for distributed processing. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The first use is to learn about clusters. This requires learning about the software involved or the terminology and the process to actually accomplish the task. I have created a script to help bootstrap the process by installing salt and then installing other common software across the cluster. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The next use, which is one i’ve been fascinated about, is microservices. The idea behind this is when an application is needed it will be automatically put on an open server that can handle the resource draw. When the application gets overloaded, simply scale the application horizontally. This means installing another instance of the application. Then load balance the traffic among all those installed servers. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Another use is for distributed processing. Which is having a complicated problem that can be broken apart into pieces. Then send each of the pieces to a separate server to process a part of the problem, then send all the results back and combine the results. This speeds up the processing of some problems. 

<!-- /wp:paragraph -->

<!-- wp:heading -->

## The Setup for Software

<!-- /wp:heading -->

<!-- wp:paragraph -->

[Cluster Setup][1] Is the github link which contains the script and data to install a new cluster. The script started by emulating on vagrant. The script installs salt and then provisions all hosts from there. It finds all hosts using nmap and then saves them to the salt roster file. It assumes all found hosts are raspberry pi, therefore all username and passwords are the same ie username: pi, password: raspberry. Then it runs a highstate and installs all needed software including the salt minion.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The script sets up gitfs for salt as well. Gitfs is salt pulling from a github repository to dynamically decide what and how to install software and set up configurations. [This is my salt configuration.][2]

<!-- /wp:paragraph -->

<!-- wp:heading -->

## The Setup for Hardware {#mce_16}

<!-- /wp:heading -->

<!-- wp:paragraph -->

Setting up the hardware for this project was fun and simple. It required about a hundred dollars, but was an excellent investment.

<!-- /wp:paragraph -->

<!-- wp:image {"id":160} --><figure class="wp-block-image">

<img src="https://i0.wp.com/52projects52weeks.com/wp-content/uploads/2019/01/IMG_20181225_225744.jpg?fit=525%2C394&ssl=1" alt="" class="wp-image-160" /><figcaption>Completed Raspberry pi cluster</figcaption></figure> <!-- /wp:image -->

<!-- wp:paragraph -->

The cluster requires 

<!-- /wp:paragraph -->

<!-- wp:list -->

*   4 raspberry pi 3b+
*   4 sd cards
*   4 small usb to micro usb cords
*   4 small ethernet cords
*   A raspberry pi tower
*   A usb hub
*   An ethernet hub

<!-- /wp:list -->

<!-- wp:image {"id":161} --><figure class="wp-block-image">

<img src="https://i0.wp.com/52projects52weeks.com/wp-content/uploads/2019/01/IMG_20181225_215500.jpg?fit=525%2C394&ssl=1" alt="USB Hub" class="wp-image-161" /><figcaption>USB Hub</figcaption></figure> <!-- /wp:image -->

<!-- wp:image {"id":162} --><figure class="wp-block-image">

<img src="https://i1.wp.com/52projects52weeks.com/wp-content/uploads/2019/01/IMG_20181225_215009.jpg?fit=525%2C394&ssl=1" alt="Ethernet Hub" class="wp-image-162" /><figcaption>Ethernet Hub</figcaption></figure> <!-- /wp:image -->

<!-- wp:image {"id":164,"align":"right","width":426,"height":320} -->

<div class="wp-block-image">
  <figure class="alignright is-resized"><img src="https://i1.wp.com/52projects52weeks.com/wp-content/uploads/2019/01/IMG_20181225_214632.jpg?fit=525%2C394&ssl=1" alt="First layer pi" class="wp-image-164" width="426" height="320" /><figcaption>Raspberry Pi on first layer</figcaption></figure>
</div>

<!-- /wp:image -->

<!-- wp:image {"id":163,"align":"left","width":420,"height":315} -->

<div class="wp-block-image">
  <figure class="alignleft is-resized"><img src="https://i1.wp.com/52projects52weeks.com/wp-content/uploads/2019/01/IMG_20181225_213547.jpg?fit=525%2C394&ssl=1" alt="Peel off film" class="wp-image-163" width="420" height="315" /><figcaption>Peel off Film</figcaption></figure>
</div>

<!-- /wp:image -->

<!-- wp:paragraph -->

The first step is to peel off the film and screw the pi into the first plate. Do this for all 4 raspberry pi's. Then add the separators and screw them in, stacking each one on top of the other. Once they are all screwed in, then stack the whole tower on top of the ethernet hub and then put that on top of the usb hub. Finally connect all the wires and load up the headless raspbian operating system on the sd cards as well as the ssh file in the boot directory.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->

<!-- wp:heading -->

## The Future

<!-- /wp:heading -->

<!-- wp:paragraph {"align":"left"} -->

<p style="text-align:left">
  In the future i'd like to PXE boot the raspberry pis so that is an automatic process.
</p>

<!-- /wp:paragraph -->

 [1]: https://github.com/unsupo/cluster-setup
 [2]: https://github.com/unsupo/cluster-setup-salt