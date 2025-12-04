+++
title = 'A Simple Guide to Choosing Licenses for Your Projects'
date = 2024-12-13T00:00:00+00:00
draft = false
tags = ['licensing', 'open-source', 'gpl', 'software-development']
+++

If you are confused about licenses like me, [this guide](https://www.gnu.org/licenses/license-recommendations.html) helps you decide on licenses for software, documentation, and other practical works. Here, I'll provide a simplified (but probably not entirely accurate) version of it.

1. **General Rule of Thumb**:
   - If you're modifying an existing project, stick with its original license unless you have a really good reason to change it.
   - If you do switch licenses, make sure it's allowed and make it clear which parts use which license.

2. **For Software**:
   - Use **GNU GPL (General Public License)** for most projects to make sure users have the freedom to use, share, and modify your work.
   - For small programs (under 300 lines), use **Apache License 2.0**—it's simpler and less restrictive.
   - For server software, pick **GNU AGPL (Affero GPL)** to ensure users can access the source code even when running online.

3. **For Libraries**:
   - Use **LGPL (Lesser GPL)** if you expect proprietary software to use your library.
   - Use **GPL** for libraries with specialized or unique use cases.

4. **For Documentation**:
   - Use **GNU Free Documentation License (GFDL)** for big works like manuals.
   - For smaller docs, use a simpler license like **GNU all-permissive license**.

5. **For Icons, Fonts, and Other Works**:
   - If these are part of a software project, use the same license as the software.
   - If they're standalone, go for a **Creative Commons Attribution-ShareAlike (CC BY-SA)** license to keep them free and shareable.

## What is Copyleft?

Copyleft is a way to make sure that software (or other creative works) remains free for everyone to use, share, and modify. It works by allowing anyone to use your work, but with the condition that if they make changes and share it, they must also make those changes available under the same free terms.

In simpler terms: it's like sharing your recipe with friends, but telling them that if they make changes to it, they also have to share the updated recipe in the same way. This ensures that the work stays open and free for everyone.

And that's pretty much it! The GNU Project recommends these licenses to keep your work free and accessible. If you're still unsure, you can always contact their licensing team.
