# LINKS — Lab 21 (Option B)

**Học viên:** Nguyễn Trường Giang — **MSSV:** 2A202600624

## 🔗 GitHub repository

- Repo: `https://github.com/NgTrgGiang/lab21_2A202600624_NguyenTruongGiang`

## 🤗 HuggingFace Hub — LoRA adapters

> ⚠️ **TODO:** Push 3 adapter lên HF Hub (link sẽ active sau khi push).

| Rank | HuggingFace adapter URL |
|-----:|--------------------------|
| r=8  | https://huggingface.co/NgTruongGiang/lab21-r8  |
| r=16 | https://huggingface.co/NgTruongGiang/lab21-r16 |
| r=64 | https://huggingface.co/NgTruongGiang/lab21-r64 |

## 📤 Cách push adapter lên HF Hub

Chạy trong notebook (hoặc Python) sau khi đã `huggingface-cli login`:

```python
from huggingface_hub import login
login()  # dán HF token (Settings > Access Tokens > write)

from peft import PeftModel  # hoặc dùng trainer/model đang có sẵn

# Cách 1: push trực tiếp từ thư mục adapter đã lưu local
from huggingface_hub import upload_folder, create_repo
for rank in [8, 16, 64]:
    repo_id = f"NgTruongGiang/lab21-r{rank}"
    create_repo(repo_id, exist_ok=True)
    upload_folder(
        repo_id=repo_id,
        folder_path=f"r{rank}",          # thư mục adapter local
        ignore_patterns=["checkpoint-*", "optimizer.pt", "*.pth"],  # chỉ push adapter, bỏ optimizer/checkpoint
    )
    print("pushed:", repo_id)

# Cách 2: nếu model còn trong RAM
# ft_model.push_to_hub("NgTruongGiang/lab21-r16")
# tokenizer.push_to_hub("NgTruongGiang/lab21-r16")
```

## ✅ Cách load lại adapter từ Hub (để verify)

```python
from peft import AutoPeftModelForCausalLM
model = AutoPeftModelForCausalLM.from_pretrained("NgTruongGiang/lab21-r16")
```
