# MacOS setup

1\. Install Requirements

Here we use homebrew to install basic prerequisites (not including Erlang/Elixir/Node which are installed via asdf

<pre class="language-bash"><code class="lang-bash"><strong>brew update
</strong><strong>brew install node
</strong><strong>brew install nvm
</strong><strong>brew install automake
</strong>brew install libtool
brew install gcc
brew install gmp
</code></pre>

### 2. Install asdf

[asdf ](https://asdf-vm.com/manage/plugins.html)is the easiest way to install and set versioning for Erlang and Elixir.

```bash
brew install asdf
asdf plugin add erlang
asdf plugin add elixir
asdf plugin add nodejs
```

Check your elixir version (`elixir -v`). If there is no response or the proper version is not showing up, you may need to reshim asdf.

```
asdf reshim  
export PATH=~/.asdf/shims:$PATH
```

Check your node version (node -v). If the incorrect version does not show

### 3. Install and start PostgreSQL-14

```bash
brew install postgresql@14
brew services start postgresql@14
```



