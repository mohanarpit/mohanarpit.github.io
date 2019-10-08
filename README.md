# Personal Website & Blog on Jekyll

This website is hosted via Github Pages. It uses Jekyll as a static site generator.

## Requirements:
1. Ruby 2.6.0
2. Bundler
3. Jekyll

## 1. Install Jekyll & Bundler
```
gem install --user-install bundler jekyll
```

## 2. Add Ruby gems to PATH
```
export PATH=$PATH:$HOME/.gem/ruby/2.6.0/bin
```

## 3. Install all the gems
```
bundle install
```

## 4. Run the website locally
```
bundle exec jekyll serve
```

### 5. Preview the site
Preview your site, in your web browser, navigate to `http://localhost:4000`.
