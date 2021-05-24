---
layout: default
nav_order: 1
toc: true
---

# HTA MEL Atlas 1

The HTA MEL Atlas 1 dataset contains images and other data being used for
construction of an atlas of human melanoma under the auspices of the
[Human Tumor Atlas Network](https://humantumoratlas.org/). Advanced solid
cancers are complex assemblies of tumor, immune, and stromal cells that invade
adjacent tissue and spread to distant sites. We use highly multiplexed tissue
imaging, spatial statistics, and machine learning to identify cell types and
states underlying morphological features of known diagnostic and prognostic
significance in melanoma. This includes the tumor invasive margin,
where tumor, normal, and immune cells compete and were diverse immunosuppressive
environments are found.

## Contents
* [Data Overviews](#data-overviews)
* [Data Explorations](#data-explorations)
* [About Minerva](#about-minerva)


## Data overviews

**NOTE! These Data Overviews provide access to minimally processed
Level 2 images with no annotation or quality control. Click any of the
following thumbnail images for an interactive view of the
full-resolution images.**

{%
    assign overviews = site.minerva
    | where_exp: "item", "item.hide != true"
    | where_exp: "item", "item['exhibit type'] != 'story'"
%}
{%
    assign stories = site.minerva
    | where_exp: "item", "item.hide != true"
    | where_exp: "item", "item['exhibit type'] == 'story'"
    | sort: "nav_order"
%}

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));">

{% for overview in overviews %}
{% assign thumbnail_name = overview.url
    | split: '/'
    | last
    | replace: '.html', '.jpg'
    | prepend: "thumbnail-"
%}
{% assign caption =
    overview.url
    | split: '/'
    | last
    | replace: '-he-overview.html', ' – H&E'
    | replace: '-overview.html', ' – CyCIF'
    | replace: 'mel', 'MEL'
%}
<figure class="figure-story">
    <a href="{{ overview.url | prepend: site.baseurl }}">
        <img src="{{ site.baseurl }}/images/{{ thumbnail_name }}">
        <figcaption>{{ caption }}</figcaption>
    </a>
</figure>
{% endfor %}

</div>


## Data Explorations

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));">

{% for story in stories %}
{% assign thumbnail_name = story.url
    | split: '/'
    | last
    | replace: '.html', '.jpg'
    | prepend: "thumbnail-"
%}
{% assign caption =
    story.url
    | split: '/'
    | last
    | replace: '.html', ''
%}
<figure class="figure-story">
    <a href="{{ story.url | prepend: site.baseurl }}">
        <img src="{{ site.baseurl }}/images/{{ thumbnail_name }}">
        <figcaption>{{ caption }}</figcaption>
    </a>
</figure>
{% endfor %}

</div>


## About Minerva
### Exploring the primary image data in Nirmal et al.

The images in Nirmal et al. (2021) comprise a ~2.3 TB dataset with some images as
large as 1 gigapixel.  We provide access to this information without restriction
(as required by the NCI Moonshot effort) but it is not in a convenient form for
reviewers or general users to explore. The open source Minerva software was
designed for the [Human Tumor Atlas Network
(HTAN)](https://humantumoratlas.org/) by the Laboratory of Systems Pharmacology
to address this problem.

Minerva enables intuitive real-time exploration of very large (gigapixel)
high-plex images in the cloud using a web browser. With Minerva, users can pan
around and magnify areas of an image and switch between channels. Minerva does
not require the installation of any software and is therefore secure; browsing
is also anonymous. Users interested in the tool are welcome to explore the
[documentation](https://github.com/labsyspharm/minerva-story/wiki), the
[software publication](https://joss.theoj.org/papers/10.21105/joss.02579), and a
description of [digital
docents](https://www.biorxiv.org/content/10.1101/2020.03.27.001834v2) in
general.

We provide two types of Minerva stories with this paper:

1. “*Data Overviews*” provide access to minimally processed Level 2 images with
   annotation and interpretation kept to a bare minimum.
2. “*Data Explorations*” are like museum guides and exploit the digital docents
   in Minerva to guide readers through the complexities of a large image dataset
   via a series of narrated stories and waypoints. Both written and audio
   narration are supported, as well as free exploration. These will be linked to
   individual figure panels in the final manuscript.
