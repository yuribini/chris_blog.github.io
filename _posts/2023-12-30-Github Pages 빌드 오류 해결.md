---
title: 2023-12-30-Github Pages 빌드 오류 해결
date: 2023-12-30 09:42:00 +09:00
categories: [Git/GitHub, Troubleshooting]
tags:
  [Git, Github, BuildError, Error: The process '/opt/hostedtoolcache/Ruby/3.3.0/x64/bin/bundle' failed with exit code 5 ]
---

# Github Pages 빌드 오류 내용

    - github Pages를 잘 사용하고 있었는데. 어느날 블로그 포스팅 글이 push 이후 build가 되지 않는 현상이 발생했다.
    에러 메세지는 아래 내용이며 해결 방법은 간단하다.

```bash
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

current directory:
/home/runner/work/yuribini.github.io/yuribini.github.io/vendor/bundle/ruby/3.3.0/gems/google-protobuf-3.25.1/ext/google/protobuf_c
rake
RUBYARCHDIR\=/home/runner/work/yuribini.github.io/yuribini.github.io/vendor/bundle/ruby/3.3.0/extensions/x86_64-linux/3.3.0/google-protobuf-3.25.1
RUBYLIBDIR\=/home/runner/work/yuribini.github.io/yuribini.github.io/vendor/bundle/ruby/3.3.0/extensions/x86_64-linux/3.3.0/google-protobuf-3.25.1
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems.rb:259:in
`find_spec_for_exe': can't find gem rake (>= 0.a) with executable rake
(Gem::GemNotFoundException)
from /opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems.rb:278:in
`activate_bin_path'
	from /opt/hostedtoolcache/Ruby/3.3.0/x64/bin/rake:25:in `<main>'

rake failed, exit code 1

Gem files will remain installed in
/home/runner/work/yuribini.github.io/yuribini.github.io/vendor/bundle/ruby/3.3.0/gems/google-protobuf-3.25.1
for inspection.
Results logged to
/home/runner/work/yuribini.github.io/yuribini.github.io/vendor/bundle/ruby/3.3.0/extensions/x86_64-linux/3.3.0/google-protobuf-3.25.1/gem_make.out

/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/builder.rb:125:in
`run'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/rake_builder.rb:30:in
`build'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/builder.rb:193:in
`build_extension'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/builder.rb:227:in
`block in build_extensions'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/builder.rb:224:in
`each'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/ext/builder.rb:224:in
`build_extensions'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/rubygems/installer.rb:852:in
`build_extensions'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/rubygems_gem_installer.rb:76:in
`build_extensions'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/rubygems_gem_installer.rb:28:in
`install'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/source/rubygems.rb:205:in
`install'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/installer/gem_installer.rb:54:in
`install'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/installer/gem_installer.rb:16:in
`install_from_spec'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/installer/parallel_installer.rb:132:in
`do_install'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/installer/parallel_installer.rb:123:in
`block in worker_pool'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/worker.rb:62:in
`apply_func'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/worker.rb:57:in
`block in process_queue'
  <internal:kernel>:187:in `loop'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/worker.rb:54:in
`process_queue'
/opt/hostedtoolcache/Ruby/3.3.0/x64/lib/ruby/3.3.0/bundler/worker.rb:90:in
`block (2 levels) in create_threads'

An error occurred while installing google-protobuf (3.25.1), and Bundler cannot
continue.

In Gemfile:
  jekyll-theme-chirpy was resolved to 6.3.1, which depends on
    jekyll-archives was resolved to 2.2.1, which depends on
      jekyll was resolved to 4.3.3, which depends on
        jekyll-sass-converter was resolved to 3.0.0, which depends on
          sass-embedded was resolved to 1.69.6, which depends on
            google-protobuf
Error: The process '/opt/hostedtoolcache/Ruby/3.3.0/x64/bin/bundle' failed with exit code 5
```

<br>
<br>

# 해결 방법
- GitHub Actions 설정에서 사용된 Ruby 버전(ruby-version: 3)과 로컬 환경의 Ruby 버전 불일치가 원인이였다.
- .github/workflows 내부 .yml 파일의 ruby-version을 3.2로 변경하여 로컬 환경과 일치시키니 해결되었다.

<br>

![ruby_commit](/images/ruby_commit.png)
