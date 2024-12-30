---
title: '[Homebrew] Own Homebrew Command Using JS'
date: 2024-10-09 06:00:00 +0000
categories: [Homebrew]
tags: [Homebrew]
author: Shuhaku
mermaid: true
---

> This post may contain errors.  
> Please use it for reference only.
{: .prompt-warning }

## Preparations
- Github Account
- Homebrew 

### What is homebrew?
Homebrew is a package manager for macOS and Linux that makes it easy to install, update, and manage software with simple commands like brew install [package]. It helps developers quickly set up tools and libraries without affecting system files.

You can use any language such as C, Go, JS, etc., but here we will use JS.

## **1. Creating a Homebrew Program**
Create a folder and initialize it with Git and npm.
```
mkdir my-homebrew-program
cd my-homebrew-program
git init

npm init -y
npm install
```

---

Create an executable file.(index.js)

```js
#!/usr/bin/env node
console.log("Hello, Homebrew!");
```

---

Grant execution permissions
```
chmod +x index.js
```

---

Additionally, create README and LICENSE files.

As a result, the my-homebrew-program folder will contain three files: index.js, README, and LICENSE.

At this point, create a repository on your GitHub named ‘my-homebrew-program.’

```
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-name/my-homebrew-program
git push -u origin main
```

Connect the repository and push the changes.

---

Additionally, create a tag in advance for future use.

```
git tag -a v1.0.0 -m "First release"
git push --tags
```

---

## **2. Creating a Homebrew Formula**
Create a new repository named 'homebrew-myprogram.'  
Create a new folder and create a formula file.

```
mkdir homebrew-myprogram
cd homebrew-myprogram
git init
```

---

Create a myprogram.rb file.

```
class Myprogram < Formula
  desc "Description of your program"           # A short description of what your program does
  homepage "https://github.com/your-name/my-homebrew-program"   # Link to your program's GitHub repo
  url "https://github.com/your-name/my-homebrew-program/archive/refs/tags/v1.0.0.tar.gz"   # The URL to download your program's tarball (a compressed archive of the code)
  sha256 "THE_SHA256_HASH_OF_THE_TARBALL"      # The SHA256 hash of the tarball file (you'll generate this)
  license "MIT"                                # The license type for your program

  def install
    bin.install "index.js" => "myprogram"      # Tells Homebrew to install the `index.js` file as `myprogram`
  end

  test do
    system "#{bin}/myprogram", "--version"     # A simple test to check if the program was installed successfully
  end
end
```

Now, you need to generate the sha256 hash value, which is the hash of the tarball compressed version of the my-homebrew-program folder created earlier.

Create a tarball.
```
tar -czvf my-homebrew-program.tar.gz my-homebrew-program/
```

Obtain the hash value.
```
shasum -a 256 path/to/tarball.tar.gz
```

Once the hash value is generated, insert it into the sha256.
Similarly, commit the changes and push them to the homebrew-myprogram repository.

At this point, you will have two repositories: my-homebrew-program (the executable program) and homebrew-myprogram (the formula).

Navigate to the my-homebrew-program repository and click on the ‘Releases’ tab.
Select the tag you created earlier, write a title and description, and then attach the tar file of my-homebrew-program you generated earlier. Finally, publish the release.

At this point, the tarball file must be the same as the one from which the sha256 hash value was obtained.

Once publishing is complete, open the terminal on your Mac.

```
brew tap your-name/myprogram
brew install myprogram

myprogram
```

![1_myprogram](/assets/img/dev/2024-10-09/1_myprogram.png)

If you enter the commands in order, you’ll be able to call the program using the command you created (which is really cool...:)
