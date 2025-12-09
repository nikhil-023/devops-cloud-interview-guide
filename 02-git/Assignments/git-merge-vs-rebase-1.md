# Setup: Create a test repository
mkdir test-repo
cd test-repo
git init
git config user.email "test@example.com"
git config user.name "Test User"

# Create initial commit on main
echo "main content" > file.txt
git add file.txt
git commit -m "Initial commit on main"

# Create and switch to feature branch
git checkout -b feature-branch

# Make changes on feature branch
echo "feature content" > feature.txt
git add feature.txt
git commit -m "Add feature"

# Switch back to main
git checkout main

# Make different changes on main (optional - for testing conflicts)
echo "main update" >> file.txt
git add file.txt
git commit -m "Update main"

# Merge feature branch into main
git merge feature-branch

# View merge result
git log --oneline --graph --all

# To undo the merge if needed:
git reset --hard HEAD~1