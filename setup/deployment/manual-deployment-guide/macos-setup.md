# MacOS setup

{% hint style="success" %}
🚗  [Autoscout is now available](../../../using-blockscout/autoscout.md), providing a simple one-click explorer deployment with Blockscout's optimized hosting infrastructure. Use it for early testing, modifications, and launching a full production-grade explorer. [**Get Started Now**](../../../using-blockscout/autoscout.md) **and have your explorer up-and-running in minutes.**
{% endhint %}

{% hint style="info" %}
These instructions use homebrew for setup. [Install homebrew](https://docs.brew.sh/Installation) if you don't already have it installed.
{% endhint %}

### 1. Install Requirements

Use homebrew to install basic prerequisites (not including Erlang/Elixir/Node which are installed via asdf)

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

### 3. Install and start PostgreSQL-14

```bash
brew install postgresql@14
brew services start postgresql@14
```

### 4. Clone the Blockscout repository and install .tool-version from the repository

```bash
git clone https://github.com/blockscout/blockscout blockscout-backend
cd blockscout-backend
asdf install
```

Check your elixir version (`elixir -v`) and node version (`node -v`).\
\
You should have the following installed:

* `Elixir 1.15.x (compiled with Erlang/OTP 26)`
* `Node v18.17.1`

If there is no response or the proper version is not showing up, you may need to reshim asdf. Please check the [asdf docs](https://asdf-vm.com/) for further info if this doesn't work.

```
asdf reshim  
export PATH=~/.asdf/shims:$PATH
```

Once complete, recheck your versions and proceed with deployment.

{% hint style="success" %}
**🎉 You are ready for manual deployment!** [**Proceed to step 3 in the "Prepare the Backend section**](./#1.-prepare-the-backend)**"**
{% endhint %}
