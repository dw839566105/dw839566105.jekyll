---
layout:     post
title:      Matplotlib templates
subtitle:   
date:       2021-08-11
author:     DW
header-img: img/post/post-bg-2.jpg
catalog: true
tags:
    - Matplotlib
---

# [Template]：Matplotlib
> 教程 [Tutorial](https://matplotlib.org/stable/tutorials/index.html) 
> 示例 [examples](https://matplotlib.org/stable/gallery/index.html)

## Import
```
    import matplotlib.pyplot as plt
```
#### add a figure
get figure and axis
```
    fig, ax = plt.figure(tight_layout, figsize, dpi)
    fig = plt.gcf()
    ax = plt.gca()

    fig, axs = plt.subplots(2, 2, subplot_kw=dict(projection="polar"))
    axs[0, 0].plot(x, y)
    axs[1, 1].scatter(x, y)

    ax1 = plt.subplot(2, 2, 1)

    import matplotlib.gridspec as gridspec
    from mpl_toolkits.axes_grid.inset_locator import inset_axes
    fig = plt.figure(constrained_layout=False, figsize=(6,6))
    spec = gridspec.GridSpec(ncols=2, nrows=2, figure=fig, hspace=0.1, wspace=0.35)
    ax1 = fig.add_subplot(spec[0, 0])
    ax2 = fig.add_subplot(spec[0, 1])
    ax3 = fig.add_subplot(spec[1, 0])
    ax4 = fig.add_subplot(spec[1, 1])
```
fixed axis height weight ratio
```
    from mpl_toolkits.axes_grid1 import Divider, Size
    fig = plt.figure(figsize=(6,4.5))
    h = [Size.Fixed(1.0), Size.Scaled(1.), Size.Fixed(.2)]
    v = [Size.Fixed(0.7), Size.Scaled(1.), Size.Fixed(.5)]
    divider = Divider(fig, (0, 0, 1, 1), h, v, aspect=False)
    ax = fig.add_axes(divider.get_position(),
                  axes_locator=divider.new_locator(nx=1, ny=1))

```

define colorbar
```
    from matplotlib import cm
    from matplotlib.colors import ListedColormap, LinearSegmentedColormap
    viridis = cm.get_cmap('jet', 256)
    newcolors = viridis(np.linspace(0, 1, 65536))
    wt = np.array([1, 1, 1, 1])
    newcolors[:25, :] = wt
    newcmp = ListedColormap(newcolors)
```
share colorbar
```
    fig.colorbar(im1[3], ax=[ax1, ax2, ax3, ax4], aspect=40, shrink = 0.85)
```

x y ratio
```
    ax2.set_aspect('equal')
```
xy tick
```
    ax2.tick_params(which="both", bottom=True)
    ax2.tick_params(which="both", left=True)
```
