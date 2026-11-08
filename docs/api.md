# API 参考

!!! note "仅用于文档展示"
    以下内容是接口契约示例，用于练习描述请求和响应。本网站没有运行后端，直接访问 `/api/docs` 不会返回这些 JSON。

## 查询文档列表

| 项目 | 说明 |
| --- | --- |
| 请求方法 | `GET` |
| 请求路径 | `/api/docs` |
| 功能 | 按关键词查询文档，并返回分页列表 |
| 成功响应类型 | `application/json` |

### 查询参数

| 参数 | 类型 | 必填 | 默认值 | 约束 |
| --- | --- | --- | --- | --- |
| `q` | string | 否 | 空字符串 | 按标题关键词过滤 |
| `page` | integer | 否 | `1` | 大于等于 1 |
| `page_size` | integer | 否 | `10` | 1 至 100 |

### 请求示例

```http
GET /api/docs?q=指南&page=1&page_size=10 HTTP/1.1
Accept: application/json
```

### 成功响应示例

```json
{
  "items": [
    {
      "id": 1,
      "title": "使用指南",
      "path": "guide/",
      "summary": "本地预览、严格构建与自动发布步骤"
    }
  ],
  "page": 1,
  "page_size": 10,
  "total": 1
}
```

`items` 表示当前页条目，`total` 表示筛选后的总数量。没有匹配结果时返回 `200` 和空数组，`total` 为 `0`。示例中的 `path` 相对于站点根目录，因此对应本网站的[使用指南](guide.md)。

### 参数错误示例

请求 `page=0` 时，契约约定返回 `400 Bad Request`：

```json
{
  "error": {
    "code": "INVALID_PARAMETER",
    "message": "page 必须大于等于 1",
    "field": "page"
  }
}
```

## 编写接口文档时的检查点

接口文档应同时说明参数类型、默认值、合法范围和错误行为。只有一个成功 JSON 时，调用方仍然不知道怎样分页、怎样判断无结果，以及参数错误时会发生什么。本页补充这些约定，使示例更接近一份可供实现者和调用方共同检查的契约。

继续阅读：[项目说明](about.md) · [使用指南](guide.md) · [返回首页](index.md)
