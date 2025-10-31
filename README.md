# terraform-azure-demo

This repository holds a small Terraform demo for Azure. A few notes on running Terraform locally and keeping the repo clean.

## Prerequisites (Windows)
- Install Terraform (choose one):
  - Chocolatey: `choco install terraform`
  - Download from HashiCorp: https://developer.hashicorp.com/terraform/downloads and extract `terraform.exe` to a folder on your PATH (e.g. `C:\terraform`).

## Make Terraform available in VS Code
1. Ensure `terraform --version` works in Command Prompt.
2. If it works in CMD but not in VS Code, restart VS Code after installing so the integrated terminal picks up your updated PATH.
3. If needed, add the install directory to your user PATH and restart VS Code.

## Typical commands
```powershell
terraform init
terraform plan -out plan.tfplan
terraform apply "plan.tfplan"
terraform destroy
```

## Git best-practices for Terraform projects
- Do NOT commit the `.terraform/` directory, provider binaries, or local state files.
- This repo includes a `.gitignore` that excludes:
  - `.terraform/`
  - `terraform.tfstate` and backups
  - `.terraform.lock.hcl`

If a large file gets committed ( >100MB ), GitHub will reject the push. Use Git LFS for large assets, or remove the file from history using `git filter-repo` or BFG and then force-push. A `backup-main` branch was created before cleaning the repository.

## When something goes wrong
- If your push is rejected with `GH001: Large files detected`: remove the file from history and re-push (or use Git LFS).
- Useful links:
  - Git LFS: https://git-lfs.github.com/
  - git-filter-repo: https://github.com/newren/git-filter-repo

## Notes
- Keep only `.tf` files, module code, and CI/workflow files in the repo. Use remote state (Azure Storage, Terraform Cloud) to store state safely.

If you want, I can also create a short CONTRIBUTING.md with a checklist to follow before committing.
