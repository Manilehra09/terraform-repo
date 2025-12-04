provider "github" {
  token = var.git_token

}


# Create a new GitHub repository
resource "github_repository" "my_repo" {
  name        = "demo-terraform-repo1"
  description = "This repository was created using Terraform"
  visibility  = "public"
  auto_init   = true
}
resource "github_branch" "development" {
  repository = "${github_repository.my_repo.name}"
  branch     = "development"
}
#  Create files in the repository
resource "github_repository_file" "testfile1" {
  repository          = github_repository.my_repo.name
  file                = "terstfile1.md"
  content             = "This is a test file 1"
  commit_message      = "Add README.md via Terraform"
  overwrite_on_create = true
}

resource "github_repository_file" "testfile2" {
  repository          = github_repository.my_repo.name
  file                = ".testfile2.md"
  content             = "This is a test file 2"
  commit_message      = "Add .gitignore via Terraform"
  overwrite_on_create = true
}

resource "github_repository_file" "testfile3" {
  repository          = github_repository.my_repo.name
  branch = github_branch.development.branch 
  file                = "terstfile3.md"
  content             = "This is a test file 3"
  commit_message      = "Added via Terraform"
  overwrite_on_create = true
  autocreate_branch = true
}
