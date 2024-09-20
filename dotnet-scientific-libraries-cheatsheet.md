# .NET Scientific Libraries Cheat Sheet

## Table of Contents
- [.NET Scientific Libraries Cheat Sheet](#net-scientific-libraries-cheat-sheet)
  - [Table of Contents](#table-of-contents)
  - [Math.NET Numerics](#mathnet-numerics)
  - [Microsoft.ML](#microsoftml)
  - [TensorFlow.NET](#tensorflownet)
  - [Numpy.NET](#numpynet)
  - [Pandas.NET](#pandasnet)
  - [ScottPlot](#scottplot)
  - [Plotly.NET](#plotlynet)
  - [.NET Interactive Notebooks](#net-interactive-notebooks)

## Math.NET Numerics

Math.NET Numerics is a foundational library for scientific computing in .NET.

[Documentation](https://numerics.mathdotnet.com/)

```csharp
using MathNet.Numerics.LinearAlgebra;
using MathNet.Numerics.Statistics;

// Create a matrix
var matrix = Matrix<double>.Build.Random(3, 3);

// Solve linear equation
var vector = Vector<double>.Build.Random(3);
var result = matrix.Solve(vector);

// Basic statistics
var data = new[] { 1.0, 2.0, 3.0, 4.0, 5.0 };
var mean = data.Mean();
var stdDev = data.StandardDeviation();

// Interpolation
var interpolation = Interpolate.Linear(new double[] { 1, 2, 3 }, new double[] { 10, 20, 30 });
var interpolatedValue = interpolation.Interpolate(2.5);
```

## Microsoft.ML

Microsoft.ML is a cross-platform machine learning framework for .NET.

[Documentation](https://docs.microsoft.com/en-us/dotnet/machine-learning/)

```csharp
using Microsoft.ML;
using Microsoft.ML.Data;

public class IrisData
{
    [LoadColumn(0)] public float SepalLength;
    [LoadColumn(1)] public float SepalWidth;
    [LoadColumn(2)] public float PetalLength;
    [LoadColumn(3)] public float PetalWidth;
    [LoadColumn(4)] public string Label;
}

public class IrisPrediction
{
    [ColumnName("PredictedLabel")] public string PredictedLabels;
}

// Create MLContext
var mlContext = new MLContext();

// Load data
var dataView = mlContext.Data.LoadFromTextFile<IrisData>("iris.csv", hasHeader: true, separatorChar: ',');

// Create pipeline
var pipeline = mlContext.Transforms.Conversion.MapValueToKey("Label")
    .Append(mlContext.Transforms.Concatenate("Features", nameof(IrisData.SepalLength), nameof(IrisData.SepalWidth), nameof(IrisData.PetalLength), nameof(IrisData.PetalWidth)))
    .Append(mlContext.MulticlassClassification.Trainers.SdcaMaximumEntropy())
    .Append(mlContext.Transforms.Conversion.MapKeyToValue("PredictedLabel"));

// Train model
var model = pipeline.Fit(dataView);

// Make prediction
var predictor = mlContext.Model.CreatePredictionEngine<IrisData, IrisPrediction>(model);
var prediction = predictor.Predict(new IrisData { SepalLength = 5.1f, SepalWidth = 3.5f, PetalLength = 1.4f, PetalWidth = 0.2f });
```

## TensorFlow.NET

TensorFlow.NET is a .NET Standard binding for TensorFlow, a popular machine learning framework.

[Documentation](https://tensorflownet.readthedocs.io/)

```csharp
using Tensorflow;
using static Tensorflow.Binding;

// Create tensors
var hello = tf.constant("Hello, TensorFlow!");

// Create a session and run
using (var sess = tf.Session())
{
    var result = sess.run(hello);
    Console.WriteLine(result);
}

// Simple neural network
var X = tf.placeholder(tf.float32, shape: (-1, 3));
var W = tf.Variable(tf.random_normal(shape: (3, 2)));
var b = tf.Variable(tf.zeros(shape: (2)));
var y = tf.matmul(X, W) + b;

var init = tf.global_variables_initializer();
using (var sess = tf.Session())
{
    sess.run(init);
    var result = sess.run(y, new FeedItem(X, new float[,] { { 1, 2, 3 }, { 4, 5, 6 } }));
    Console.WriteLine(result);
}
```

## Numpy.NET

Numpy.NET provides a .NET API for NumPy, allowing you to work with multi-dimensional arrays.

[Documentation](https://github.com/SciSharp/Numpy.NET)

```csharp
using Numpy;

// Create arrays
var a = np.array(new int[] { 1, 2, 3 });
var b = np.array(new int[,] { { 1, 2, 3 }, { 4, 5, 6 } });

// Array operations
var c = np.dot(a, b);
var d = np.mean(b, axis: 1);

// Broadcasting
var e = a + b;

// Linear algebra
var f = np.linalg.inv(np.array(new double[,] { { 1, 2 }, { 3, 4 } }));
```

## Pandas.NET

Pandas.NET is a .NET port of the pandas library, providing data manipulation and analysis tools.

[Documentation](https://github.com/SciSharp/Pandas.NET)

```csharp
using Pandas.NET;

// Create a DataFrame
var df = pd.DataFrame(new 
{
    A = new[] { 1, 2, 3, 4 },
    B = new[] { "a", "b", "c", "d" },
    C = new[] { 4.5, 5.5, 6.5, 7.5 }
});

// Basic operations
var columnA = df["A"];
var firstTwoRows = df.Head(2);
var filteredDf = df[df["A"] > 2];

// GroupBy and aggregation
var grouped = df.GroupBy("B").Mean();

// Merge DataFrames
var df2 = pd.DataFrame(new 
{
    B = new[] { "a", "b", "e" },
    D = new[] { 10, 20, 30 }
});
var merged = pd.merge(df, df2, on: "B", how: "left");
```

## ScottPlot

ScottPlot is a plotting library for .NET applications.

[Documentation](https://scottplot.net/)

```csharp
using ScottPlot;

// Create a plot
var plt = new Plot(600, 400);

// Add data
double[] xs = DataGen.Consecutive(51);
double[] ys = DataGen.Sin(51);
plt.AddScatter(xs, ys);

// Customize the plot
plt.Title("Sine Wave");
plt.XLabel("X Axis");
plt.YLabel("Y Axis");

// Save the plot
plt.SaveFig("sine_wave.png");
```

## Plotly.NET

Plotly.NET is a powerful plotting library for .NET that allows you to create interactive and publication-quality graphs. It supports F# and C# and can be used in various .NET environments.

[Documentation](https://plotly.net/)

```csharp
using Plotly.NET;
using Plotly.NET.LayoutObjects;

// Create a simple line plot
var lineChart = Chart.Line<int, int, string>(
    x: new[] { 1, 2, 3, 4, 5 },
    y: new[] { 1, 4, 9, 16, 25 },
    Name: "Square function"
);

// Customize the layout
lineChart.WithTitle("Square Function Plot")
         .WithXAxisStyle(title: "X Axis")
         .WithYAxisStyle(title: "Y Axis");

// Show the chart (when using in a notebook or interactive environment)
lineChart.Show();

// Save the chart as an HTML file
lineChart.SaveHtml("line_chart.html");

// Create a more complex chart with multiple traces
var trace1 = Chart.Line<int, int, string>(
    x: new[] { 1, 2, 3, 4 },
    y: new[] { 10, 15, 13, 17 },
    Name: "Trace 1"
);

var trace2 = Chart.Scatter<int, int, string>(
    x: new[] { 2, 3, 4, 5 },
    y: new[] { 16, 5, 11, 9 },
    Mode: Plotly.NET.StyleParam.Mode.Markers,
    Name: "Trace 2"
);

var combinedChart = Chart.Combine(new[] { trace1, trace2 })
    .WithTitle("Combined Line and Scatter Plot")
    .WithXAxisStyle(title: "X Axis")
    .WithYAxisStyle(title: "Y Axis");

combinedChart.Show();

// Create a 3D surface plot
var z = new double[,]
{
    { 10, 20, 10 },
    { 20, 30, 20 },
    { 30, 40, 30 }
};

var surfacePlot = Chart.Surface<double>(z)
    .WithTitle("3D Surface Plot")
    .WithXAxisStyle(title: "X Axis")
    .WithYAxisStyle(title: "Y Axis")
    .WithZAxisStyle(title: "Z Axis");

surfacePlot.Show();

// Create a box plot
var boxPlot = Chart.BoxPlot<int, int, string>(
    x: new[] { 1, 1, 1, 1, 1, 2, 2, 2, 2, 2 },
    y: new[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 }
)
.WithTitle("Box Plot")
.WithXAxisStyle(title: "Category")
.WithYAxisStyle(title: "Value");

boxPlot.Show();
```

Plotly.NET offers a wide range of chart types and customization options. Here are some key features:

1. Supports various chart types: line, scatter, bar, histogram, box plot, heatmap, 3D plots, and more.
2. Interactive plots with zooming, panning, and hover information.
3. Easy customization of chart layout, axes, legends, and other elements.
4. Support for both static and dynamic data sources.
5. Ability to combine multiple charts and create subplots.
6. Export options to various formats, including HTML, SVG, and PNG.
7. Integration with .NET Interactive Notebooks for easy visualization in Jupyter-like environments.

To use Plotly.NET in your project, you can install it via NuGet:

```
dotnet add package Plotly.NET
```

For F# projects, you might want to use the F#-specific package:

```
dotnet add package Plotly.NET.Interactive
```

Plotly.NET provides a powerful and flexible way to create data visualizations in .NET, comparable to the capabilities of Python's Plotly library.

## .NET Interactive Notebooks

.NET Interactive Notebooks allow you to create and share documents that contain live code, equations, visualizations, and narrative text.

[Documentation](https://github.com/dotnet/interactive)

To use .NET Interactive Notebooks:

1. Install the .NET Interactive Notebooks VS Code extension.
2. Create a new notebook with a .ipynb extension.
3. Select C# as the kernel.

Example notebook cell:

```csharp
#r "nuget: ScottPlot, 4.1.27"
using ScottPlot;

var plt = new Plot(600, 400);
double[] xs = DataGen.Consecutive(51);
double[] ys = DataGen.Sin(51);
plt.AddScatter(xs, ys);
plt.Title("Sine Wave");
plt.SaveFig("sine_wave.png");
Display("sine_wave.png");
```

This cheat sheet covers a range of popular .NET libraries for scientific computing, data analysis, and visualization. Each section includes a brief description, a link to the documentation, and example code snippets to help you get started with these libraries.
