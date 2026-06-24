# 数据可视化

> 本文档整合了以下源文件：dataviz.md

---

## 来源：dataviz.md

本文整理了主流的开源数据可视化框架、库和软件，按编程语言和用途分类，便于快速选型和学习。

---

## 一、JavaScript 工具

### 1.1 图表库

| 名称 | 链接 | 说明 |
|------|------|------|
| ApexCharts | [apexcharts.com](https://apexcharts.com/) | 现代交互式 SVG 图表 |
| Chart.js | [chartjs.org](https://www.chartjs.org/) | 基于 Canvas 的轻量图表库 |
| Chartist.js | [chartist-js](https://gionkunz.github.io/chartist-js/) | 响应式图表，浏览器兼容性好 |
| dc.js | [GitHub](https://github.com/dc-js/dc.js) | 多维图表，原生支持 crossfilter |
| Dygraphs | [dygraphs.com](https://dygraphs.com/) | 交互式折线图，适合大数据集 |
| ECharts | [GitHub](https://github.com/ecomfe/echarts) | 高度可定制、支持大数据集 |
| Epoch | [GitHub](https://github.com/epochjs/epoch) | 实时图表 |
| Google Charts | [developers.google.com](https://developers.google.com/chart) | 浏览器和移动端交互式图表 |
| G2 | [g2plot.antv.vision](https://g2plot.antv.vision/en) | 基于图形语法的交互式图表库（阿里 AntV） |
| GraphicsJS | [graphicsjs.org](http://www.graphicsjs.org) | 轻量图形库，基于 SVG/VML |
| lit-line | [GitHub](https://github.com/apinet/lit-line) | SVG 折线图 Web Component，轻量快速 |
| MetricsGraphics.js | [metricsgraphicsjs.org](https://metricsgraphicsjs.org/) | 针对时间序列数据优化 |
| NVD3 | [GitHub](https://github.com/novus/nvd3) | 基于 D3.js 的可复用图表库 |
| Plotly.js | [GitHub](https://github.com/plotly/plotly.js/) | 声明式库，支持 20+ 图表类型 |
| TechanJS | [techanjs.org](https://techanjs.org/) | 股票和金融图表 |
| TOAST UI Chart | [GitHub](https://github.com/nhnent/tui.chart) | 功能完整，支持旧版浏览器 |
| Vizzu | [GitHub](https://github.com/vizzuhq/vizzu-lib) | 动画数据可视化与数据叙事 |

### 1.2 图/网络可视化库

| 名称 | 链接 | 说明 |
|------|------|------|
| Cola.js | [webcola](https://marvl.infotech.monash.edu/webcola/) | 基于约束优化的图表布局，兼容 D3 和 SVG.js |
| Cytoscape.js | [js.cytoscape.org](https://js.cytoscape.org/) | 图绘制库，由 Cytoscape 核心开发者维护 |
| Sigma.js | [sigmajs.org](https://sigmajs.org/) | 专注图绘制的 JS 库 |
| VivaGraph | [GitHub](https://github.com/anvaka/VivaGraphJS) | JavaScript 图绘制库 |
| G6 | [GitHub](https://github.com/antvis/g6) | 图可视化引擎，支持 JS/TS（阿里 AntV） |
| diagram.js | [GitHub](https://github.com/bpmn-io/diagram-js) | BPMN 建模器底层图表库 |
| Uber React Digraph | [GitHub](https://github.com/uber/react-digraph) | 基于 React 的有向图库（Uber） |

### 1.3 地图工具

| 名称 | 链接 | 说明 |
|------|------|------|
| CARTO | [GitHub](https://github.com/CartoDB/cartodb) | 地理空间数据存储与可视化 |
| Cesium | [GitHub](https://github.com/AnalyticalGraphicsInc/cesium) | WebGL 3D 地球与地图 |
| Deck.gl | [deck.gl](https://deck.gl/) | WebGL 大数据集地理空间分析框架 |
| L7 | [GitHub](https://github.com/antvis/L7) | 大规模 WebGL 地理空间可视化框架（阿里 AntV） |
| L7 Plot | [GitHub](https://github.com/antvis/L7Plot) | 地理空间可视化图表库（阿里 AntV） |
| DataMaps | [GitHub](https://github.com/markmarkoh/datamaps) | 基于 D3.js 的交互式 SVG 地图 |
| Dipper | [GitHub](https://github.com/antvis/dipper) | 基于 L7 的地图应用开发框架（阿里 AntV） |
| Leaflet | [leafletjs.com](https://leafletjs.com) | 移动端友好的交互式地图库 |
| Mapael | [GitHub](https://github.com/neveldo/jQuery-Mapael) | 基于 raphael.js 的 jQuery 矢量地图插件 |

### 1.4 D3 生态

D3 生态资源丰富，详见 [Awesome D3](https://github.com/wbkd/awesome-d3)。

### 1.5 React 生态

| 名称 | 链接 | 说明 |
|------|------|------|
| BizCharts | [GitHub](https://github.com/alibaba/BizCharts) | 基于 G2 和 React 的数据可视化库（阿里） |
| Graphin | [GitHub](https://github.com/antvis/Graphin) | 基于 React/TS 的图可视化库，底层使用 G6（阿里） |
| React-vis | [GitHub](https://github.com/uber/react-vis) | React 数据可视化组件（Uber） |
| Recharts | [GitHub](https://github.com/recharts/recharts) | 声明式 React D3 图表组件 |
| Victory | [formidable.com](https://formidable.com/open-source/victory/) | 可组合的交互式数据可视化组件 |
| nivo | [GitHub](https://github.com/plouc/nivo) | React 数据可视化组件，支持同构渲染，[在线演示](https://nivo.rocks) |
| React Svg Textures | [GitHub](https://github.com/finnfiddle/react-svg-textures) | Textures.js 的 React 移植版，支持同构 |
| DevExtreme React Chart | [devexpress](https://devexpress.github.io/devextreme-reactive/react/chart/) | 高性能 React 图表插件，支持 Bootstrap/Material Design |

### 1.6 React Native

| 名称 | 链接 | 说明 |
|------|------|------|
| F2 | [GitHub](https://github.com/antvis/F2) | 移动端交互式图表库（阿里 AntV） |

### 1.7 其他 JS 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| Graphology | [GitHub](https://github.com/graphology/graphology) | 通用图对象库，为图可视化提供基础支持 |
| Piecon | [GitHub](https://github.com/lipka/piecon) | 在网站图标（favicon）中显示饼图 |
| Textures.js | [textures](https://riccardoscalco.github.io/textures/) | 创建 SVG 纹理图案 |
| Timeline.js | [timeline.knightlab](https://timeline.knightlab.com/) | 创建交互式时间线 |
| Vega | [vega.github.io](https://vega.github.io/vega/) | 可视化语法，声明式创建交互式可视化 |
| Vega-Lite | [vega-lite](https://vega.github.io/vega-lite/) | 高级图形语法，简洁 JSON 语法快速生成可视化 |
| Vis.js | [visjs.org](https://visjs.org/) | 动态可视化库，支持时间线、网络图（2D/3D） |

---

## 二、Android 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| DecoView | [GitHub](https://github.com/bmarrdev/android-DecoView-charting) | 动画环形图表库 |
| MPAndroidChart | [GitHub](https://github.com/PhilJay/MPAndroidChart) | 功能强大且易用的图表库 |
| WilliamChart | [GitHub](https://github.com/diogobernardino/WilliamChart) | 简洁图表库 |

---

## 三、C++ 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| LargeVis | [GitHub](https://github.com/lferry007/LargeVis) | 大规模高维数据可视化实现 |
| PlotJuggler | [GitHub](https://github.com/facontidavide/PlotJuggler) | 基于 Qt5/Qwt 的开源绘图应用 |
| VTK | [GitLab](https://gitlab.kitware.com/vtk/vtk/blob/master/README.md) | 3D 图形、图像处理与可视化开源库 |

---

## 四、Go 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| svgo | [GitHub](https://github.com/ajstarks/svgo) | Go 语言 SVG 生成库 |
| plot | [GitHub](https://github.com/gonum/plot) | Go 语言绘图 API |
| go-echarts | [GitHub](https://github.com/chenjiandongx/go-echarts) | Go 语言数据可视化库，封装 ECharts |

---

## 五、iOS 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| BEMSimpleLineGraph | [GitHub](https://github.com/Boris-Em/BEMSimpleLineGraph) | 高度可定制的交互式折线图 |
| Charts | [GitHub](https://github.com/danielgindi/Charts) | MPAndroidChart 的 iOS 移植版，双平台可用 |
| JBChartView | [GitHub](https://github.com/Jawbone/JBChartView) | 折线图和柱状图库 |
| PNChart | [GitHub](https://github.com/kevinzhow/PNChart) | 简洁美观的图表库 |

---

## 六、机器学习工具

| 名称 | 链接 | 说明 |
|------|------|------|
| TensorWatch | [GitHub](https://github.com/microsoft/tensorwatch) | 数据科学与机器学习调试和可视化工具（微软） |

---

## 七、Python 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| Altair | [altair-viz](https://altair-viz.github.io/) | 声明式统计可视化，基于 Vega-Lite |
| Bokeh | [bokeh](https://bokeh.pydata.org/en/latest/) | Python 交互式 Web 绘图 |
| Chartify | [GitHub](https://github.com/spotify/chartify) | Bokeh 封装，简化图表创建（Spotify） |
| diagram | [GitHub](https://github.com/tehmaze/diagram) | 使用 UTF-8 字符的文本模式图表 |
| ggplot | [GitHub](https://github.com/yhat/ggpy) | 基于 R ggplot2 的 Python 绑定 |
| glumpy | [GitHub](https://github.com/glumpy/glumpy) | OpenGL 科学可视化库 |
| HoloViews | [holoviews.org](https://holoviews.org/) | 基于标注数据的声明式可视化 |
| ipychart | [GitHub](https://github.com/nicohlr/ipychart) | Jupyter Notebook 中使用 Chart.js |
| Mayavi | [docs.enthought.com](https://docs.enthought.com/mayavi/mayavi/) | 交互式科学数据可视化与 3D 绘图 |
| matplotlib | [matplotlib.org](https://matplotlib.org/) | Python 2D 绘图基础库 |
| missingno | [GitHub](https://github.com/ResidentMario/missingno) | 数据集完整性可视化工具，基于 matplotlib |
| Plotly | [plot.ly/python](https://plot.ly/python/) | 基于 plotly.js 的交互式 Web 可视化 |
| pptk | [GitHub](https://github.com/heremaps/pptk) | 2D/3D 点云可视化与处理 |
| PyQtGraph | [pyqtgraph.org](https://www.pyqtgraph.org/) | 交互式实时 2D/3D 绘图与科学工程组件 |
| PyVista | [GitHub](https://github.com/pyvista/pyvista) | 3D 绘图与网格分析，VTK 封装接口 |
| seaborn | [seaborn](https://seaborn.pydata.org/) | 统计图形库，生成美观的信息图表 |
| toyplot | [readthedocs](https://toyplot.readthedocs.io/en/stable/) | 轻量 Python 绘图工具包 |
| three.py | [GitHub](https://github.com/stemkoski/three.py/) | 基于 PyOpenGL 的 3D 库，受 Three.js 启发 |
| Veusz | [veusz](https://veusz.github.io/) | Python 多平台 GUI 绘图工具 |
| VisPy | [vispy.org](https://vispy.org/) | 基于 OpenGL 的高性能科学可视化 |
| VTK | [vtk.org](https://www.vtk.org/) | 3D 计算机图形、图像处理与可视化，含 Python 接口 |
| pandas-profiling | [GitHub](https://github.com/pandas-profiling/pandas-profiling) | 生成统计分析报告与可视化 |
| pyecharts | [GitHub](https://github.com/pyecharts/pyecharts) | ECharts 的 Python 绑定 |

---

## 八、R 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| ggplot2 | [tidyverse](https://ggplot2.tidyverse.org/) | 基于图形语法的绘图系统 |
| ggvis | [rstudio](https://ggvis.rstudio.com/) | 语法类似 ggplot2 的交互式图形包 |
| lattice | [r-forge](https://lattice.r-forge.r-project.org) | R 的网格图形系统 |
| plotly | [GitHub](https://github.com/ropensci/plotly) | 交互式图表，支持 ggplot2 输出增强 |
| rbokeh | [hafen](https://hafen.github.io/rbokeh/) | Bokeh 的 R 接口 |
| rgl | [CRAN](https://cran.r-project.org/web/packages/rgl/index.html) | 基于 OpenGL 的 3D 可视化 |
| shiny | [rstudio](https://shiny.rstudio.com) | 创建交互式应用和可视化的框架 |
| visNetwork | [datastorm-open](https://datastorm-open.github.io/visNetwork/) | 交互式网络可视化 |

---

## 九、Ruby 工具

| 名称 | 链接 | 说明 |
|------|------|------|
| Chartkick | [GitHub](https://github.com/ankane/chartkick) | 一行代码创建图表 |

---

## 十、标记语言工具

| 名称 | 链接 | 说明 |
|------|------|------|
| Mermaid.js | [mermaid-live-editor](https://mermaidjs.github.io/mermaid-live-editor) | 类 Markdown 脚本语言生成图表 |
| WaveDrom | [wavedrom.com](https://wavedrom.com/) | 从文本描述绘制时序图/波形图 |

---

## 十一、跨平台通用工具

| 名称 | 链接 | 说明 |
|------|------|------|
| Charted | [GitHub](https://github.com/mikesall/charted) | 自动从数据文件生成可分享图表 |
| Gephi | [GitHub](https://github.com/gephi/gephi) | 大规模图可视化与操作平台 |
| Kepler.gl | [kepler.gl](https://kepler.gl/) | 大规模地理空间分析工具 |
| Mermaid | [GitHub](https://github.com/knsv/mermaid) | 从文本生成图表和流程图 |
| RAW | [rawgraphs.io](https://rawgraphs.io) | 从 CSV/Excel 文件创建 Web 可视化 |
| Spark | [GitHub](https://github.com/holman/spark) | Shell 迷你图工具，[多语言实现](https://github.com/holman/spark/wiki/Alternative-Implementations) |
| Visual-Insights | [GitHub](https://github.com/ObservedObserver/visual-insights) | 自动洞察提取与可视化规范推荐 |
| X6 | [x6.antv.vision](https://x6.antv.vision/en) | 图编辑引擎，支持 DAG/ER/流程图等（阿里 AntV） |
| Graphviz | [graphviz.org](https://graphviz.org/) | 开源图可视化命令行工具，支持 SVG/PDF/交互式 Web 输出 |

---

## 十二、学习资源

### 12.1 推荐书籍

| 书名 | 作者 | 说明 |
|------|------|------|
| Design for Information | Isabel Meirelles | 信息设计入门 |
| The Best American Infographics 2014 | Gareth Cook | 信息图表精选 |
| The Grammar of Graphics | Leland Wilkinson | 可视化理论基础 |
| The Visual Display of Quantitative Information | Edward Tufte | 经典数据可视化理论 |
| The Wall Street Journal Guide to Information Graphics | Dona M. Wong | 信息图表实用指南 |
| Visualization Analysis and Design | Tamara Munzner | 可视化分析与设计 |
| Interactive Data Visualization for the Web | Scott Murray | D3.js 在线教程，[可在线阅读](https://chimera.labs.oreilly.com/books/1230000000345) |
| Data Visualization Toolkit | Barrett Austin Clark | 使用 D3/Rails/Postgres/Leaflet |
| Data Visualisation: A Handbook for Data Driven Design | Andy Kirk | 数据驱动设计手册 |

### 12.2 图表类型参考目录

| 名称 | 链接 | 说明 |
|------|------|------|
| The Data Visualization Catalogue | [datavizcatalogue.com](https://www.datavizcatalogue.com) | 数据可视化方法集合，含优缺点分析 |
| Data Viz Project | [datavizproject.com](https://datavizproject.com) | 可视化项目参考 |
| The R Graph Gallery | [r-graph-gallery.com](https://www.r-graph-gallery.com) | R 图形示例库 |
| From Data to Viz | [data-to-viz.com](https://www.data-to-viz.com) | 从数据到可视化的选型指南 |
| Chartopedia | [anychart.com](https://www.anychart.com/chartopedia) | 图表百科 |
| Interactive Chart Chooser | [depictdatastudio.com](https://depictdatastudio.com/charts/) | 交互式图表选择器 |

### 12.3 Wikipedia 参考页面

| 主题 | 链接 |
|------|------|
| 数据可视化技术 | [Wikipedia](https://en.wikipedia.org/wiki/Data_visualization#Techniques) |
| 图形方法列表 | [Wikipedia](https://en.wikipedia.org/wiki/List_of_graphical_methods) |
| 图表类型 | [Wikipedia](https://en.wikipedia.org/wiki/Chart#Types) |
| 图形类型 | [Wikipedia](https://en.wikipedia.org/wiki/Diagram#Gallery_of_diagram_types) |
| 绘图类型 | [Wikipedia](https://en.wikipedia.org/wiki/Plot_(graphics)#Types_of_plots) |

### 12.4 播客

| 名称 | 链接 | 说明 |
|------|------|------|
| Data Stories | [datastori.es](https://datastori.es/) | 数据可视化播客 |
| DataFramed | [datacamp.com](https://www.datacamp.com/community/podcast) | DataCamp 数据科学播客 |
| Data Viz Today | [dataviztoday.com](https://dataviztoday.com/) | 数据可视化实践播客 |

### 12.5 推荐网站与博客

| 名称 | 链接 | 说明 |
|------|------|------|
| Data For Visualization | [dataforvisualization.com](https://dataforvisualization.com/) | 从软件开发者视角讲数据叙事 |
| Data Visualization Society | [datavisualizationsociety.com](https://www.datavisualizationsociety.com/) | 数据可视化专业社区 |
| eagereyes | [eagereyes.org](https://eagereyes.org/) | 可视化研究博客 |
| EvergreenData | [stephanieevergreen.com](https://stephanieevergreen.com/) | 数据可视化实用指南 |
| FlowingData | [flowingdata.com](https://flowingdata.com/) | 数据可视化与统计分析 |
| Information is Beautiful | [informationisbeautiful.net](https://www.informationisbeautiful.net/) | 信息图表与数据可视化 |
| Junk Charts | [junkcharts.typepad.com](https://junkcharts.typepad.com/) | 图表案例分析，探讨图表为何有效/无效 |
| Makeover Monday | [makeovermonday.co.uk](https://www.makeovermonday.co.uk/) | 每周数据可视化改进挑战 |
| The Pudding | [pudding.cool](https://pudding.cool/) | 数据驱动的视觉叙事 |
| Truth & Beauty Operations | [truth-and-beauty.net](https://truth-and-beauty.net/) | 可视化设计工作室 |
| UW Interactive Data Lab Papers | [idl.cs.washington.edu](https://idl.cs.washington.edu/papers) | 华盛顿大学交互数据实验室论文 |
| vis4.net | [vis4.net](https://www.vis4.net/blog/) | 可视化与数据新闻 |

---

## 关键要点

1. **选型依据**：根据项目需求选择工具。Web 端优先考虑 ECharts/Plotly/D3；Python 数据分析首选 matplotlib/seaborn/Plotly；R 语言首选 ggplot2。
2. **交互式 vs 静态**：需要交互式 Web 可视化时，优先考虑 ECharts、Plotly、Vega-Lite；静态图表使用 matplotlib、ggplot2 即可。
3. **大数据集处理**：处理大规模数据时，关注 Deck.gl（地理数据）、Dygraphs（时间序列）、LargeVis（高维降维）等专项优化工具。
4. **图形语法理论**：理解 Grammar of Graphics（图形语法）有助于深入掌握 ggplot2、G2、Vega-Lite 等声明式可视化工具的设计理念。
5. **阿里 AntV 生态**：G2、G6、L7、X6 构成完整的可视化体系，覆盖图表、图分析、地理空间和图编辑四大领域。
6. **图表选型参考**：利用 The Data Visualization Catalogue、From Data to Viz 等目录网站，根据数据特征快速选择合适的图表类型。


---
