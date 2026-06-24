# Cooklang：食谱标记语言

## 简介

Cooklang 是一种专为编写食谱而设计的标记语言。它提供了一种结构化的方式来在纯文本文件中定义食材、厨具和步骤说明。结合 Cooklang 应用和工具生态系统，它实现了版本控制的、可移植的食谱管理。本教程涵盖语法、工具和实际工作流程。

## 为什么选择 Cooklang

| 优势 | 描述 |
|------|------|
| 纯文本 | 人类可读的食谱格式 |
| 结构化数据 | 可解析的食材和用量 |
| 版本控制 | 使用 Git 跟踪食谱变更 |
| 可移植性 | 跨应用和平台工作 |
| 可扩展 | 自定义元数据和标签 |

## 语法概览

### 基本结构

Cooklang 食谱有两个主要部分：元数据和步骤。

```cooklang
>> source: https://example.com/recipe
>> servings: 4
>> prep time: 15 minutes
>> cook time: 30 minutes

Add @olive oil{1%tbsp} to a large pan over medium heat.

Add @garlic{3%clove}s, minced, and cook for @~{1%minute}.

Add @chicken breast{500%g} and cook until golden on each side, about @~{5%minutes} per side.

Season with @salt{} and @pepper{} to taste.

Serve with @rice{2%cups} and @steamed broccoli{300%g}.
```

## 元数据头

元数据行以 `>>` 开头，定义食谱属性。

| 键 | 描述 | 示例 |
|----|------|------|
| source | 食谱来源 URL | `https://example.com` |
| servings | 份数 | `4` |
| prep time | 准备时间 | `15 minutes` |
| cook time | 烹饪时间 | `30 minutes` |
| total time | 总时间 | `45 minutes` |
| cuisine | 菜系 | `Italian` |
| course | 餐次 | `Main` |
| tags | 食谱标签 | `quick, weeknight` |
| author | 食谱作者 | `Chef Name` |

### 元数据示例

```cooklang
>> source: https://example.com/pasta
>> servings: 2
>> prep time: 10 minutes
>> cook time: 20 minutes
>> cuisine: Italian
>> course: Main
>> tags: pasta, quick, weeknight
>> difficulty: easy
```

## 食材

### 基本食材

食材以 `@` 为前缀，可以包含用量和单位。

| 语法 | 描述 | 示例 |
|------|------|------|
| `@name` | 仅名称 | `@salt` |
| `@name{quantity%unit}` | 名称带用量 | `@flour{2%cups}` |
| `@name{quantity}` | 用量无单位 | `@eggs{3}` |
| `@name{%unit}` | 单位无用量 | `@salt{}`（少许） |

### 食材示例

```cooklang
@olive oil{2%tbsp}
@onion{1%large}, diced
@garlic{3%clove}s, minced
@diced tomatoes{400%g}
@chicken breast{500%g}
@salt{} and @pepper{} to taste
@fresh basil{10%leaf}ves
@parmesan cheese{50%g}, grated
```

### 复数处理

Cooklang 自动处理复数形式。

| 输入 | 渲染为 |
|------|--------|
| `@egg{2}` | 2 eggs |
| `@clove{3}` | 3 cloves |
| `@leaf{10}` | 10 leaves |
| `@tomato{4}` | 4 tomatoes |

## 厨具

厨具项目以 `~` 为前缀。

| 语法 | 描述 | 示例 |
|------|------|------|
| `@~name` | 厨具项目 | `@~large pot` |
| `@~name{size}` | 带尺寸的厨具 | `@~pan{12-inch}` |

### 厨具示例

```cooklang
Heat @olive oil{1%tbsp} in a @~large skillet over medium heat.

Transfer to a @~baking dish{9x13-inch}.

Whisk in a @~mixing bowl.

Bake in @~oven at @~temperature{375%°F} for @~{25%minutes}.
```

## 计时器

计时器用 `~` 定义并指定持续时间。

| 语法 | 描述 | 示例 |
|------|------|------|
| `@~{duration%unit}` | 命名计时器 | `@~{10%minutes}` |
| `@~name{duration%unit}` | 带标签的计时器 | `@~bake{25%minutes}` |

### 计时器示例

```cooklang
Simmer for @~{15%minutes}, stirring occasionally.

Bake at 375°F for @~bake{25%minutes} until golden.

Let rest for @~rest{5%minutes} before serving.

Marinate for @~{2%hours} or overnight.
```

## 步骤说明

### 编写步骤

步骤说明是带有嵌入食材、厨具和计时器的纯文本。

```cooklang
Bring a @~large pot of @water{4%liters} to a boil.

Add @spaghetti{400%g} and cook for @~{8%minutes} until al dente.

Meanwhile, heat @olive oil{2%tbsp} in a @~pan over medium heat.

Add @pancetta{150%g} and cook for @~{5%minutes} until crispy.

Drain the pasta, reserving @pasta water{1%cup}.

Toss the pasta with the pancetta and @egg{4} mixture.

Add @parmesan cheese{100%g} and toss until creamy.

Season with @black pepper{} and serve immediately.
```

## 完整食谱示例

```cooklang
>> title: Classic Spaghetti Carbonara
>> source: https://example.com/carbonara
>> servings: 4
>> prep time: 10 minutes
>> cook time: 20 minutes
>> cuisine: Italian
>> course: Main
>> tags: pasta, italian, classic

Bring a @~large pot of @water{4%liters} to a rolling boil.

Add @spaghetti{400%g} and cook according to package directions for @~{8%minutes}.

While the pasta cooks, heat @olive oil{2%tbsp} in a @~large skillet over medium heat.

Add @pancetta{150%g}, cut into small cubes, and cook for @~pancetta{5%minutes} until crispy.

In a @~mixing bowl, whisk together @egg{4} and @egg yolk{2}.

Add @parmesan cheese{100%g}, freshly grated, to the egg mixture and whisk to combine.

When the pasta is done, reserve @pasta water{1%cup} and drain the rest.

Add the hot pasta to the skillet with pancetta. Toss to combine.

Remove from heat and quickly add the egg and cheese mixture, tossing constantly.

Add @pasta water{1%tbsp} at a time if the sauce is too thick.

Season generously with @black pepper{} and serve immediately.

Garnish with extra @parmesan cheese{} and @fresh parsley{}.
```

## 工具和应用

### 命令行工具

| 工具 | 描述 | 平台 |
|------|------|------|
| cooklang-cli | 官方 CLI 解析器 | 跨平台 |
| cooklang-rs | Rust 实现 | 跨平台 |
| cookparse | Python 解析器 | 跨平台 |

### 移动应用

| 应用 | 平台 | 功能 |
|------|------|------|
| CookBook | iOS、Android | 食谱浏览、购物清单 |
| Mela | iOS | 食谱管理、膳食计划 |
| Recette | iOS | Cooklang 原生应用 |

### Web 应用

| 应用 | 描述 | URL |
|------|------|-----|
| Cooklang.org | 官方网站 | cooklang.org |
| CookViewer | 食谱查看器 | 在线 |

## 购物清单

Cooklang 可以从食谱生成购物清单。

### 生成的购物清单

来自上面的 carbonara 食谱：

| 食材 | 用量 | 单位 |
|------|------|------|
| Water | 4 + 1 | liters、cup |
| Spaghetti | 400 | g |
| Olive oil | 2 | tbsp |
| Pancetta | 150 | g |
| Egg | 4 | whole |
| Egg yolk | 2 | whole |
| Parmesan cheese | 100 | g |
| Black pepper | - | to taste |
| Fresh parsley | - | garnish |

## 多食谱膳食计划

组合多个食谱用于膳食计划。

```cooklang
>> title: Weeknight Italian Dinner
>> serves: 4

Main Course: #carbonara
Side: #garlic_bread
Salad: #caesar_salad
Dessert: #tiramisu
```

## 变体和替代

记录食谱变体。

```cooklang
## Variations

### Vegetarian
Replace @pancetta{150%g} with @mushroom{200%g}, sliced.

### Gluten-Free
Use @gluten-free spaghetti{400%g} instead of regular pasta.

### Dairy-Free
Replace @parmesan cheese{100%g} with @nutritional yeast{3%tbsp}.
```

## 组织食谱

### 目录结构

```
recipes/
  italian/
    carbonara.cook
    bolognese.cook
    margherita.cook
  asian/
    pad_thai.cook
    fried_rice.cook
    curry.cook
  desserts/
    chocolate_cake.cook
    apple_pie.cook
    cookies.cook
  breakfast/
    pancakes.cook
    omelette.cook
```

## Git 集成

### 版本控制食谱

```bash
# 初始化仓库
cd recipes
git init

# 跟踪变更
git add .
git commit -m "Add carbonara recipe"

# 更新食谱
git add italian/carbonara.cook
git commit -m "Update carbonara: adjust cooking time"

# 查看历史
git log --oneline italian/carbonara.cook
```

## 转换现有食谱

### 从纯文本到 Cooklang

转换前：
```
Spaghetti Carbonara

Ingredients:
- 400g spaghetti
- 150g pancetta
- 4 eggs
- 100g parmesan cheese
- 2 tbsp olive oil
- Black pepper

Instructions:
1. Cook spaghetti in salted water.
2. Fry pancetta until crispy.
3. Mix eggs and cheese.
4. Combine pasta with pancetta.
5. Add egg mixture off heat.
6. Season and serve.
```

转换后：
```cooklang
>> title: Spaghetti Carbonara
>> servings: 4

Cook @spaghetti{400%g} in @salted water{}.

Fry @pancetta{150%g} in @olive oil{2%tbsp} until crispy.

Mix @egg{4} and @parmesan cheese{100%g}.

Combine pasta with pancetta.

Add egg mixture off heat.

Season with @black pepper{} and serve.
```

## 总结

Cooklang 提供了一种结构化的人类可读的食谱标记语言。使用 `@` 表示带用量的食材，`~` 表示厨具和计时器，`>>` 表示元数据。生态系统包括解析器、移动应用和 Web 查看器。将食谱存储在 Git 中进行版本控制，并从解析的食材自动生成购物清单。
