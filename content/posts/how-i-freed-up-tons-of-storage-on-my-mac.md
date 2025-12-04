+++
title = 'How I Freed Up Tons of Storage on My Mac'
date = 2025-08-24T00:00:00+00:00
draft = false
tags = ['mac', 'storage', 'cleanup', 'devtools', 'performance']
+++

My Mac was almost full. It said that **"Documents" used 39 GB**, but I didn't know what was taking so much space. As a software developer, I have tools like **npm, Docker, and Homebrew** that keep files to work faster. These files can get very big. Here's how I fixed it.

## Step 1: Look at Documents

I checked my Documents folder in Finder, but the files there were much smaller than 39 GB. Then I used Terminal:

```bash
du -sh ~/Documents/* | sort -h
```

This shows the size of each file and folder. Most were small. So the big files were **hidden in caches and tools**.

## Step 2: Clear Developer Tool Caches

### 1. npm (Node.js)

```bash
du -sh ~/.npm
npm cache clean --force
```

This freed **3.5 GB**.

### 2. Docker

```bash
docker system df
docker builder prune
```

My Docker cache alone was **19 GB**!

### 3. Homebrew

```bash
du -sh ~/Library/Caches/Homebrew
brew cleanup
```

This cleared hundreds of MBs.

### 4. VSCode

```bash
rm -rf ~/Library/Application\ Support/Code/Cache/*
rm -rf ~/Library/Application\ Support/Code/CachedData/*
rm -rf ~/Library/Application\ Support/Code/User/workspaceStorage/*
```

This freed about **5 GB**.

## Step 3: Remove Old Tools You Don't Use

I had old versions of PHP and some apps I didn't use. I removed them:

```bash
brew uninstall php@7.1 php@7.4 php@8.0
brew uninstall --cask fig
brew uninstall nginx
```

## Step 4: Check Other Caches

Other tools also store caches:

* Python pip: `~/.cache/pip`
* Go modules: `~/go/pkg/mod/cache`
* iCloud: `~/Library/Mobile Documents`

You can check their size with:

```bash
du -sh <folder>
```

## Step 5: Keep It Clean

I now run these commands every few weeks:

```bash
npm cache clean --force
docker builder prune
brew cleanup
rm -rf ~/Library/Caches/*
```

This keeps my Mac from filling up again.

## Lessons Learned

* Most big storage is **hidden in caches**, not in Documents.
* Tools like Docker, npm, Homebrew, and VSCode can use **lots of GB**.
* Cleaning regularly can free **20–40 GB**.
* Terminal commands like `du -sh` and `docker system df` help find big files.

With these steps, my Mac now has plenty of space and runs better.
