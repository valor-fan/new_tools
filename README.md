# 企查查公司资产 Hunter 批量查询工具

该脚本可批量读取企查查（或任意来源）导出的企业名单，通过奇安信 Hunter API 自动枚举企业相关互联网资产，并对疑似后台/登录页进行二次筛查，帮助安全人员高效定位暴露面。也可直接在 VSCode、PyCharm 等代码工具中运行调试，快速验证脚本行为。

## 功能优势
- **即插即用的数据源**：支持直接使用企查查导出的 `company.xlsx`，也可将其他来源的公司列表整理为相同结构后替换。
- **双阶段资产挖掘**：先做全量资产检索，再针对敏感关键词聚焦登录入口，减少遗漏。
- **不良内容过滤与去重**：内置关键词黑名单与 IP/URL 去重逻辑，避免噪声污染结果。
- **多格式结果输出**：自动生成 TXT 与 XLSX，两类报告均保存在 `hunter_results/` 中，便于溯源与二次加工。

## 环境依赖
- Python 3.9+
- 详见 `requirements.txt`

建议使用虚拟环境：
```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

## 使用步骤
1. **准备公司列表**  
   - 将企查查导出的 Excel 重命名为 `company.xlsx`（或在脚本中调整 `EXCEL_FILE` 指向该文件）。  
   - 确保表头包含“公司名称”字段，数据位于该列下方。
2. **配置 Hunter 认证信息**  
   编辑 `hunter_Asset _Collection.py` 中 `config` 字典的 `api_key`、`account` 等项，填入个人凭证。
3. **安装依赖**  
   运行 `pip install -r requirements.txt`。
4. **执行脚本**  
   ```bash
   python "hunter_Asset _Collection.py"
   ```
5. **查看输出**  
   - `hunter_results/hunter_results.xlsx`：主查询结果  
   - `hunter_results/chinese_company_sensitive_systems.xlsx`：敏感系统/登录页  
   - `hunter_results/hunter_results.txt`：文本版摘要

## Excel 数据替换说明
- 作者默认以企查查导出的公司列表为例，仅需把自己的 `company.xlsx` 放在项目根目录即可；若文件名不同，可修改 `EXCEL_FILE` 变量。
- 也可以使用其他平台导出的数据，只要包含“公司名称”列即可兼容。

## 注意事项
- Hunter API 调用频率有限，脚本已内置随机 `sleep` 以降低触发风控的概率，可根据实际权限调整。
- 建议首次运行前先执行脚本自动的权限自检，确保 API Key 正常。
- 结果文件会覆盖旧内容，如需保留历史报告，可预先备份 `hunter_results/` 目录。

## 作者信息
- GitHub：<https://github.com/placeholder>

