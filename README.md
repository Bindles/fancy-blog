# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...


    <% if post.created_at > 1.hour.ago %>
      <%=  "[created " + time_ago_in_words(post.created_at) %> ago
      <%= post.created_at.strftime("[%m/%d/%Y (%I %M %P)]") %>
    <% else %>
      <%= post.created_at.strftime("[%m/%d/%Y (%I %M %P)]") %>
    <% end %>

        <% if post.created_at > 1.hour.ago %>
      <%= time_ago_in_words(post.created_at) %> ago
      <%= post.created_at.strftime("[%H:%M | %m/%d/%Y]") %>
    <% else %>
      <%= post.created_at.strftime("[%m/%d/%Y (%I %M %P)]") %>
    <% end %>




    <!DOCTYPE html>
<html>
  <head>
    <title>AdubbBlog</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
    <link rel="stylesheet" href="https://cdn.simplecss.org/simple.min.css">
    <%= javascript_importmap_tags %>
  </head>

  <body>
    <header>
      <%= render 'layouts/navbar' %>
    </header>
    <%= yield %>
  </body>
</html>


  <body>
    <header>
      <%= render 'layouts/alerts' %>
      <p class="notice"><%= notice %></p>
      <p class="alert"><%= alert %></p>
    </header>
    <%= yield %>
  </body>


    <body>
    <header>
      <main>
      <p class="notice"><%= notice %></p>
      <p class="alert"><%= alert %></p>
    </header>
    </main>
    <%= yield %>
  </body>

turbo_devise_controller.rb:

  class TurboDeviseController < ApplicationController
    class Responder < ActionController::Responder
      def to_turbo_stream
        controller.render(options.merge(formats: :html))
      rescue ActionView::MissingTemplate => e
        if get?
          raise e
        elsif has_errors? && default_action
          render rendering_options.merge(formats: :html, status: :unprocessable_entity)
        else
          redirect_to navigation_location
        end
      end
    end
  
    self.responder = Responder
    respond_to :html, :turbo_stream
end


appl:
<!DOCTYPE html>
<html>
  <head>
    <title>AdubbBlog</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
    <link rel="stylesheet" href="https://cdn.simplecss.org/simple.min.css">
    <%= javascript_importmap_tags %>
  </head>

  <body>
    <header>
    
    </header>
    <%= yield %>
  </body>
</html>


navbar:

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <%= link_to "Rails Blog", root_path, class:'navbar-brand'%>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <%= link_to "Home", root_path, class:'nav-link'%>
        </li>
        <li class="nav-item">
          <%= link_to "Blog", posts_path, class:"nav-link" %>
        </li>
        <li class="nav-item">
          <%= link_to "Members", 'posts#index', class:"nav-link" %>
        </li>
        <li class="nav-item">
          <%= link_to "Portfolio", 'posts#index', class:"nav-link" %>
        </li>
        <li class="nav-item">
          <%= render 'layouts/categories', categories: @nav_categories %>
        </li>
      </ul>
      <ul class="navbar-nav">
        <%= render 'search/form' %>
        <%= render 'layouts/notifications' %>
        <%= render 'user/session_manager' %>
      </ul>
    </div>
  </div>
</nav>