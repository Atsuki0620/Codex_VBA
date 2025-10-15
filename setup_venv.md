# 共通仮想環境セットアップ手順

共通環境 `C:\venvs\env-ds` を作成し、VS Code/Jupyterで使えるようにする。

**重要**: requirements.txtは `.venv\requirements.txt` にあります。

## 1. 仮想環境の作成

```powershell
# venvs ディレクトリ作成 & 仮想環境作成
New-Item -ItemType Directory -Path 'C:\venvs' -Force
python -m venv 'C:\venvs\env-ds'
```

## 2. 必要パッケージのインストール

```powershell
& 'C:\venvs\env-ds\Scripts\python.exe' -m pip install -U pip setuptools wheel ipykernel
& 'C:\venvs\env-ds\Scripts\python.exe' -m pip install -r env-ds\requirements.txt
```

## 3. Jupyterカーネル登録

```powershell
& 'C:\venvs\env-ds\Scripts\python.exe' -m ipykernel install --user --name env-ds --display-name 'Python (env-ds)'
```

## 4. プロジェクト設定

### VS Code設定ファイル作成

`.vscode/settings.json`:
```json
{
  "python.defaultInterpreterPath": "C:\\venvs\\env-ds\\Scripts\\python.exe",
  "python.venvPath": "C:\\venvs"
}
```

### ジャンクション作成

```powershell
New-Item -ItemType Junction -Path '.venv' -Target 'C:\venvs\env-ds'
```

## 完了後

VS Codeで Developer: Reload Window を実行し、Jupyterカーネルで "Python (env-ds)" を選択。

## 一括実行コマンド

```powershell
# 全て一括で実行
New-Item -ItemType Directory -Path 'C:\venvs' -Force; python -m venv 'C:\venvs\env-ds'; & 'C:\venvs\env-ds\Scripts\python.exe' -m pip install -U pip setuptools wheel ipykernel; & 'C:\venvs\env-ds\Scripts\python.exe' -m ipykernel install --user --name env-ds --display-name 'Python (env-ds)'; New-Item -ItemType Junction -Path '.venv' -Target 'C:\venvs\env-ds'
```