---
title: "NASNet architecture with tensorboard"
categories:
  - deep-learning
tags:
  - NASNet-A
  - tensorboard
  - tensorboardX
  - torchvision
  - pytorch
---

In this post I'd like to propose you to explore [NASNet-A Large network architecture](https://arxiv.org/abs/1707.07012) in the browser (better visualization is in Google Chrome):

<script src="//cdnjs.cloudflare.com/ajax/libs/polymer/0.3.3/platform.js"></script>
<script>
  function load() {{
  }}
</script>
<link rel="import" href="https://tensorboard.appspot.com/tf-graph-basic.build.html" onload=load()>
<div style="height:600px">
  <tf-graph-basic id="graph_nasnet_a_large"></tf-graph-basic>
</div>