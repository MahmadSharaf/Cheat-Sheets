- Upgrade all packages in Windows

```ps
pip freeze | %{$_.split('==')[0]} | %{pip install --upgrade $_}
```

- Upgrade env python version

```ps
python -m venv --upgrade {ENVDIR}
```