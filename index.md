# Ferret Adoption Rails Project Blog

### Wow. What a hurdle!

My Ruby-on-Rails project was inspired by a genuine need for regional ferret adoption groups to streamline their vetting and application procedures. My app provides a space where users can post information about the ferrets they own, and whether they are looking to adopt or rehome their animals.

This project was a plethora of problem solving from its very start. I'm going to skip the silly mistakes and share a few of the more technical issues I faced as I began, so that others may avoid them:

Linking to Git/github takes a few extra moments. You don't want the main project folder nested.

With the rails new command, I forgot to do the —-no test framework for my models, so before moving any further I decided to restart my project to clean this up.

I also had an issue with incompatibilities with the msgpack that was installed with rails. I found some answers on Stack Overflow here:

https://stackoverflow.com/questions/59479802/unable-to-create-a-rails-app-due-to-incompatible-library-version-load-error

... which suggested uninstalling then reinstalling msg pack. When this didn't work, I then tried "bundle install --redownload" which fixed everything.

Later on, my rails server would not start. Entering "rails s" presented a Traceback with the following error message:

"Please run rails webpacker:install Error: No such file or directory @ realpath_rec."

But running "rails webpacker:install" did not work. How annoying.

This took a few extra minutes to figure out, but since it's happened to me twice, I want to note the solution I found on Stack Overflow here: https://stackoverflow.com/questions/57891751/webpacker-configuration-file-not-found-rails-6-0-0

First had to double check Yarn, which was already installed but I ran it again with the command "npm install --global yarn." More info here: https://classic.yarnpkg.com/en/docs/install

After this, I tried "rails webpacker:install" again. This time, the installation worked. I started up my server, and I was good to go.

Or so I thought. After I routed a simple About page, the server kept showing me very strange mailbox-oriented routes. It took some foul language and a bit of searching to correctly name the problem: Active Storage.

The fix was to suppress references to Active Storage in several files. This following solution was written for Rails 5: https://stackoverflow.com/questions/49813214/disable-active-storage-in-rails-5-2/50307393#50307393

To avoid this problem, type the following when creating your new Rails app:

rails new app_name —-no test framework --skip-active-storage --skip-action-mailbox

Happy coding.
