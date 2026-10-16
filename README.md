# Tessera

Tessera 是一个 **Node.js 小工具集**：把日常用得上的独立工具集中在一个零依赖的包里。
每加一个新工具，都遵循同样的约定——独立模块、零运行时依赖、自带 TypeScript 类型。

> 目前包处于早期阶段（0.x），导出项会随版本增加；0.x 期间不保证 API 完全稳定。

## 安装

```bash
npm install @jerryduff/tessera
```

## 现有工具

### Snowflake — 分布式唯一 ID

Twitter Snowflake 算法的 BigInt 实现，返回字符串形式的 ID（避免 JS 数字精度问题）。
结构：41 位时间戳 + 5 位数据中心 + 5 位机器 + 12 位序列号。

```ts
import { Snowflake } from "@jerryduff/tessera";

const id = Snowflake.nextId();
// => "766207627628777472"
```

CommonJS 也可以直接使用：

```js
const { Snowflake } = require("@jerryduff/tessera");
```

特点：

- 起始时间戳 2021-01-01，单机每毫秒可生成 4096 个 ID，同毫秒内自增保证唯一；
- 序列号溢出时自旋等待到下一毫秒；
- 全称使用 `BigInt` 运算，ID 以字符串返回，不丢精度。

## 后续计划

这个包会继续收纳通用工具，例如编码/哈希、时间处理、字符串与集合操作等。
有新工具时会按同样的目录结构加入 `src/`，并从入口统一导出。

## 开发

```bash
npm install
npm run build   # tsc，产物输出到 dist/
```

## License

MIT
