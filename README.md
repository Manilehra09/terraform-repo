```
provider "github" {
  token = "your git tokan"

}


# Create a new GitHub repository
resource "github_repository" "my_repo" {
  name        = "demo-terraform-repo"
  description = "This repository was created using Terraform"
  visibility  = "public"
  auto_init   = true
}

#  Create files in the repository
resource "github_repository_file" "readme" {
  repository          = github_repository.my_repo.name
  file                = "README.md"
  content             = "**/*.tfstate"
  commit_message      = "Add README.md via Terraform"
  overwrite_on_create = true
}

resource "github_repository_file" "gitignore" {
  repository          = github_repository.my_repo.name
  file                = ".gitignore"
  content             = "**/*.tfstate"
  commit_message      = "Add .gitignore via Terraform"
  overwrite_on_create = true
}

```
