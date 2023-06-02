# 需要注意要将数据放在GPU上运行

在运行时可以在vscode终端 输入nvidia-smi查看当前GPU占用

### pytorch

对于pytorch框架提供下面函数来选择GPU

```python
def try_gpu(i=0):
    """Return gpu(i) if exists, otherwise return cpu()."""
    if torch.cuda.device_count() >= i + 1:
        return torch.device(f'cuda:{i}')
    return torch.device('cpu')
```
