# AChartEngine

[AChartEngine](https://code.google.com/p/achartengine/) 是一個專為 Android 做的圖表繪制套件。它支援以下圖表類型：

* LineChartView - 折線圖
* CubeLineChartView - 立方線圖
* ScatterChartView - 散點圖
* TimeChartView - 時間圖
* BarChartView - 長條圖
* BubbleChartView - 氣泡圖
* RangeBarChartView - 條形圖
* PieChartView - 圓餅圖
* DialChartView - 撥號圖
* DoughnutChartView - 圓環圖
* CombinedXYChartView - 複合圖(可合併折線圖、立方線圖、散點圖、條圖、條形圖、氣泡圖)

裡面有一個可以取得圖表物件的工廠類別： ChartFactory ，取得圖表物件之前要先準備好幾個資料，它才能幫你處理好繪圖的部分：

* XYMultipleSeriesDataset - 資料來源，需按照它的格式傳入。
* XYMultipleSeriesRenderer - 繪圖器，裡面定義了該如何畫圖的詳細內容。

另外 PieChartView 、 DoughnutChartView 和 DialChartView 繪圖方法跟其他的不一樣，所以傳入的參數就會有所不同：

* CategorySeries / MultipleCategorySeries- 資料來源。
* DefaultRenderer / DialRenderer - 繪圖器。

## Data Set

資料一開始都會先建一個集合，然後在要取得物件時傳入當參數。

## Renderer

XYMultipleSeriesRenderer 的方法：

| Method Name | Description |
| ----------- | ----------- |
| public void setApplyBackgroundColor(boolean apply) | 設定是否要有背景顏色 |
| public void setBackgroundColor(int color) | 設定內圍的背景顏色 |
| public void setMarginsColor(int color) | 設定外圍的背顏色 |
| public void setTextTypeface(java.lang.String typefaceName, int style) | 設定文字的樣式 |
| public void setShowGrid(boolean showGrid) | 設定是否要顯示網格 |
| public void setGridColor(int color) | 設定網格顏色
| public void setChartTitle(java.lang.String title) | 設定標題文字 |
| public void setLabelsColor(int color) | 設定標題文字的顏色 |
| public void setChartTitleTextSize(float textSize) | 設定標題文字的大小 |
| public void setAxesColor(int color) | 設定雙軸的顏色 |
| public void setBarSpacing(double spacing) | 設定Bar的間距 |
| public void setXLabelsAngle(float angle) | 設定X軸文字的傾斜程度 |
