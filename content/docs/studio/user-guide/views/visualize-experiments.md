# Visualize and Compare Experiments

You can visualize and compare experiments using using plots, images, charts,
etc.

## Display plots and images

You can visualize certain metrics of machine learning experiments as plots.
Usual plot examples are AUC curves, loss functions, and confusion matrices,
among others. This type of metrics files are created by users, or generated by
user data processing code, and can be defined in dvc.yaml (plots field) for
tracking (optional). Refer to the
[DVC plots documentation](/doc/command-reference/plots) for details on how to
add plots to your repositories.

### Types of plots

DVC Studio can work with two types of plots files in your repository:

1. Data series files, which can be JSON, YAML, CSV or TSV. Data from these files
   will populate your AUC curves, loss functions and other metric plots.
2. Image files in JPEG, GIF, or PNG format. These images will be displayed
   directly in DVC Studio.

You can define multiple plots in a single repository. Below is an example
snippet from a `dvc.yaml` file showing the `evaluate` stage of the DVC pipeline.

```yaml
evaluate:
  cmd: python src/evaluate.py
  deps:
    - output/data.pkl
    - output/model.h5
    - src/evaluate.py
  metrics:
    - output/metrics.json:
        cache: false
  plots:
    - output/predictions.json:
        cache: false
        template: confusion
        x: actual
        y: predicted
    - output/misclassified_samples/:
        cache: false
```

As you can see,

- metrics from `output/predictions.json` will be rendered in a confusion matrix,
- images in the `output/misclassified_samples/` directory will be displayed
  directly.

You can also specify a single image file (eg,
`output/misclassified_sample1.png`).

### How to generate plots

To generate the plots, select one or more experiments (represented by the
commits), and click on the `Show plots` button.

The plots will appear in the plots pane. If you have selected more than one
experiment, you can use the plots to compare them.

![](https://static.iterative.ai/img/studio/plots.png)

## Generate trend charts

Click on the `Trends` button to generate a plot of how the metrics changed over
the course of the different experiments. For each metric, the trend charts show
how the metric changed from one commit to another. You can include one or more
branches in the trend chart.

![](https://static.iterative.ai/img/studio/trends.png)

## Compare experiments

To compare different experiments, select two experiments (represented by the
commits), and click on the `Compare` button. The metrics, parameters and files
in the selected experiments will be displayed side by side for easy comparison.

![](https://static.iterative.ai/img/studio/compare.png)
