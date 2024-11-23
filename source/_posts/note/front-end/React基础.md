---
title: React基础概念与组件详解
link: front-end-note-React-1
catalog: true
lang: cn
tags:
  - 前端
  - React
categories:
  - [笔记,前端,React]
date: 2024-10-29 09:34:30
---
# React基础概念与组件详解

## 1. React的基本概念

### 1.1 什么是React？
React是一个用于构建用户界面的JavaScript库。它允许开发者将界面拆分成小的、独立的代码片段，这些代码片段被称为"组件"。

### 1.2 组件（Component）
- 组件是React的核心概念
- 可以把组件理解为一个独立的、可重用的UI片段
- 每个组件都可以包含自己的逻辑和样式

### 1.3 基本语法解释
```javascript
const QueryPage = () => {
  // 这是一个函数组件
  // 使用箭头函数语法
  return (
      <div></div>
    // 返回JSX代码
  );
};
```

## 2. 状态管理（State）

### 2.1 什么是State？
状态（State）是组件内部的数据存储。当状态发生变化时，React会自动重新渲染组件。

### 2.2 代码中的状态示例
```javascript
const [expandFilters, setExpandFilters] = useState(false);
const [selectedRows, setSelectedRows] = useState([]);
```
- `useState` 是React的Hook，用于声明状态
- 第一个值（如`expandFilters`）是状态值
- 第二个值（如`setExpandFilters`）是更新该状态的函数
- 括号中的值是初始状态

## 3. 组件生命周期和副作用

### 3.1 useRef Hook
```javascript
const crvDatePickerRef = useRef();
```
- useRef用于存储在组件整个生命周期内持久存在的值
- 常用于保存DOM元素引用或其他需要持久存储的值
- 修改ref不会触发组件重新渲染

### 3.2 useEffect Hook
虽然这个组件中没有明显使用useEffect，但它是React中处理副作用的重要工具：
- 用于处理组件的副作用（如API调用、订阅等）
- 在组件渲染后执行
- 可以通过依赖数组控制执行时机

## 4. 表单处理

### 4.1 Form组件
```javascript
const [form] = Form.useForm();
```
- 使用antd的Form组件管理表单状态
- Form.useForm()创建表单实例，用于管理表单数据

### 4.2 表单字段
```javascript
<Form.Item name="invoiceNumber" label="发票号码">
  <Input placeholder="请输入发票号码"/>
</Form.Item>
```
- Form.Item 是表单项容器
- name属性用于标识表单字段
- label属性显示字段标签

## 5. 页面布局

### 5.1 Grid系统

```javascript
<Row gutter={[16, 24]}>
    {/* 这里的 16 是水平间距，24 是垂直间距 */}
  <Col span={6}>
    // 内容
  </Col>
</Row>
```
- Row 和 Col 是栅格系统组件
- gutter 定义列间距
- span 定义列宽（总宽度为24）

### 5.2 组件结构
```javascript
return (
  <div style={{padding: 24}}>
    {/* 表单部分 */}
    <Form>...</Form>
    
    {/* 表格部分 */}
    <div className="query-by-invoice">
      <CrvTable />
    </div>
  </div>
);
```

### 5.3 Row标签

#### Row justify参数

在 Ant Design 的 `<Row>` 组件中，`justify` 参数用于控制行内列内容的水平对齐方式。该属性支持五种对齐方式，每种方式都对应不同的效果，具体如下：

##### 1. `justify="start"`
- **描述**：左对齐。
- **效果**：所有列内容会向行的左侧靠拢，这是默认的对齐方式。
- **适用场景**：通常在不需要特殊对齐方式的场景下使用。

```javascript
<Row justify="start">
    <Col span={6}>内容1</Col>
    <Col span={6}>内容2</Col>
    <Col span={6}>内容3</Col>
</Row>
```

##### 2. `justify="end"`
- **描述**：右对齐。
- **效果**：所有列内容会向行的右侧靠拢。
- **适用场景**：当需要将内容右对齐时（如按钮组放在右侧）。

```javascript
<Row justify="end">
    <Col span={6}>内容1</Col>
    <Col span={6}>内容2</Col>
    <Col span={6}>内容3</Col>
</Row>
```

##### 3. `justify="center"`
- **描述**：居中对齐。
- **效果**：所有列内容会在行的中间水平居中排列。
- **适用场景**：在内容需要居中显示的情况下使用。

```javascript
<Row justify="center">
    <Col span={6}>内容1</Col>
    <Col span={6}>内容2</Col>
    <Col span={6}>内容3</Col>
</Row>
```

##### 4. `justify="space-around"`
- **描述**：每个列之间的间距相等，行的两侧也有均匀的间距。
- **效果**：内容在行中会均匀分布，每个列之间的间距相等，并且行的两侧会留出相等的空白区域。
- **适用场景**：适用于多个内容需要均匀分布并且左右两侧有空白的场景。

```javascript
<Row justify="space-around">
    <Col span={6}>内容1</Col>
    <Col span={6}>内容2</Col>
    <Col span={6}>内容3</Col>
</Row>
```

##### 5. `justify="space-between"`
- **描述**：两端对齐，首尾列贴近行的两侧，其他列均匀分布。
- **效果**：行的首列和尾列会紧贴行的左右两边，中间列的间距会均匀分布。
- **适用场景**：适用于希望首尾内容贴边，而中间内容均匀分布的场景。

```javascript
<Row justify="space-between">
    <Col span={6}>内容1</Col>
    <Col span={6}>内容2</Col>
    <Col span={6}>内容3</Col>
</Row>
```

##### 总结对比

| 值              | 说明                                 | 效果                             |
| --------------- | ------------------------------------ | -------------------------------- |
| `start`         | 左对齐（默认）                       | 所有列内容左侧靠拢               |
| `end`           | 右对齐                               | 所有列内容右侧靠拢               |
| `center`        | 居中对齐                             | 所有列内容在中间水平居中         |
| `space-around`  | 每列之间的间距相等，两侧也有均匀间距 | 列之间和行两侧都有相等的空白区域 |
| `space-between` | 首尾列贴边，中间列均匀分布           | 首尾列贴行两侧，中间列均匀分布   |

### 5.4 Select标签

`<Select>` 标签是 Ant Design 提供的一个组件，用于实现下拉选择框，通常用于用户从多个选项中选择一个或多个值。它支持多种配置项，包括单选、多选、搜索等多种功能。

#### `Select` 标签的基本用法

```jsx
<Select>
  <Select.Option value="1">Option 1</Select.Option>
  <Select.Option value="2">Option 2</Select.Option>
  <Select.Option value="3">Option 3</Select.Option>
</Select>
```

#### `<Select>` 组件的常见属性

以下是一些常用的 `<Select>` 属性，它们决定了 `Select` 组件的行为和外观：

##### 1. `mode`
- **类型**：`string`
- **说明**：控制 `Select` 是否支持多选。
  - `default`：单选模式（默认模式）。
  - `multiple`：多选模式，允许用户选择多个选项。
  - `tags`：类似多选，但支持标签输入的方式，适用于输入自定义选项的场景。

  示例：
  ```jsx
  <Select mode="multiple" placeholder="请选择">
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 2. `value`
- **类型**：`any`（通常是一个单一值或数组）
- **说明**：设置当前选中的值。如果是单选，`value` 为一个字符串或数字；如果是多选，`value` 为一个数组，包含多个已选项的 `value` 值。
- **注意**：该属性通常与 `onChange` 事件一起使用，用于控制选中项的状态。

  示例：
  ```jsx
  <Select value={this.state.selectedValue} onChange={this.handleChange}>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 3. `defaultValue`
- **类型**：`any`（单值或数组）
- **说明**：设置初始值，当 `value` 没有传入时使用。类似 `value`，但是仅在初始渲染时生效，之后如果选项改变，`defaultValue` 不会更新。

  示例：
  ```jsx
  <Select defaultValue="1">
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 4. `onChange`
- **类型**：`(value: any) => void` 或 `(value: any, option: React.ReactElement) => void`
- **说明**：`onChange` 是选项发生变化时触发的回调函数，通常用于获取当前选中的值。
- **对于多选**：`value` 会是一个数组，包含所有选中的值。

  示例：
  ```jsx
  <Select onChange={this.handleSelectChange}>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 5. `placeholder`
- **类型**：`string`
- **说明**：用于设置下拉框默认显示的占位文本，当没有选中任何项时显示该文本。

  示例：
  ```jsx
  <Select placeholder="请选择">
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 6. `disabled`
- **类型**：`boolean`
- **说明**：禁用 `Select` 组件，禁用后用户不能进行任何选择。

  示例：
  ```jsx
  <Select disabled>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 7. `allowClear`
- **类型**：`boolean`
- **说明**：允许清除选择项。适用于单选模式。启用后，会显示一个清除按钮。

  示例：
  ```jsx
  <Select allowClear defaultValue="1">
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 8. `showSearch`
- **类型**：`boolean`
- **说明**：是否允许搜索，适用于选项较多的情况下，启用该功能可以帮助用户快速定位选项。仅在单选或多选模式下有效。

  示例：
  ```jsx
  <Select showSearch placeholder="请选择">
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

##### 9. `maxTagCount`
- **类型**：`number | 'responsive'`
- **说明**：当选择多个选项时，最多显示多少个选项标签。超出部分会以 `...` 展示。

  示例：
  ```jsx
  <Select mode="multiple" maxTagCount={2}>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
    <Select.Option value="3">选项3</Select.Option>
  </Select>
  ```

##### 10. `optionFilterProp`
- **类型**：`string`
- **说明**：用于搜索过滤的属性。指定在哪个属性上进行搜索（默认为 `children`）。如果选项的内容是复杂的结构，可以设置此属性来指定搜索条件。

  示例：
  ```jsx
  <Select showSearch optionFilterProp="label">
    <Select.Option value="1" label="选项1">选项1</Select.Option>
    <Select.Option value="2" label="选项2">选项2</Select.Option>
  </Select>
  ```

##### 11. `loading`
- **类型**：`boolean`
- **说明**：是否在加载数据时显示 loading 状态，适用于异步加载选项时。

  示例：
  ```jsx
  <Select loading={isLoading}>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2">选项2</Select.Option>
  </Select>
  ```

### 5.5 `<Select.Option>` 的常见属性

##### 1.`value`

- **类型**：`string | number`
- **说明**：`Select.Option` 的值，表示该选项的标识。在 `Select` 中选择某个选项时，选中的值就是这个 `value`。

##### 2.`disabled`

- **类型**：`boolean`
- **说明**：禁用该选项，禁用后无法被选中。

  示例：
  ```jsx
  <Select>
    <Select.Option value="1">选项1</Select.Option>
    <Select.Option value="2" disabled>选项2 (禁用)</Select.Option>
  </Select>
  ```

##### 3.`label`

- **类型**：`string | ReactNode`
- **说明**：为选项提供一个自定义的显示文本，常用于 `optionFilterProp` 过滤搜索时。

### 总结

`<Select>` 组件在 Ant Design 中是一个非常强大的下拉框控件，支持多种功能，如单选、多选、搜索、标签显示等。通过不同的属性，用户可以灵活地控制其显示和交互行为。在实际应用中，选择适合的属性可以大大提升用户体验，特别是在表单和数据筛选的场景中。

## 6. 数据处理和事件处理

### 6.1 查询处理
```javascript
const handleSearch = async (values) => {
  const searchValues = values || form.getFieldsValue();
  // ... 处理查询逻辑
};
```
- 处理表单提交事件
- 收集表单数据
- 调用API进行查询

### 6.2 表格处理
```javascript
const handleSelectChange = (selectedRowKeys, selectedRows) => {
  setSelectedRows(selectedRows);
};
```
- 处理表格选择变化
- 更新选中的行数据

## 7. 核心前端开发理念

### 7.1 组件化
- 将UI拆分为独立、可重用的组件
- 每个组件负责特定的功能
- 组件之间通过props传递数据

### 7.2 状态管理
- 确定哪些数据需要放在state中
- 正确选择状态的存放位置
- 通过props向下传递数据

### 7.3 单向数据流
- 数据总是从父组件流向子组件
- 子组件通过回调函数通知父组件更新数据
- 保持数据流向的清晰性

### 7.4 声明式编程
- 描述想要的结果，而不是具体的步骤
- 让React处理DOM更新
- 关注数据和业务逻辑，而不是DOM操作

## 8. 项目实际应用

这个组件实现了一个发票查询页面，主要功能包括：

1. 表单查询
   - 基本查询条件（商户、入账状态、开票日期）
   - 展开/收起的高级筛选条件

2. 数据展示
   - 表格显示查询结果
   - 支持分页和行选择
   - 固定列和可滚动

3. 交互功能
   - 条件筛选
   - 数据选择
   - 查看详情

## 9. 最佳实践建议

1. 组件设计
   - 保持组件功能单一
   - 适当拆分大组件
   - 提取可复用逻辑

2. 状态管理
   - 最小化状态数量
   - 合理放置状态位置
   - 避免状态冗余

3. 性能优化
   - 使用useCallback优化回调函数
   - 使用useMemo优化计算结果
   - 适当使用React.memo避免不必要的重渲染

4. 代码组织
   - 相关代码放在一起
   - 遵循关注点分离原则
   - 保持代码清晰可读