# Rails Girls — The Idea App

A Ruby on Rails web application built following the [Rails Girls](http://railsgirls.com/) tutorial. **The Idea App** allows authenticated users to create, browse, edit, and manage ideas—complete with image uploads and thumbnail generation—as well as post comments on ideas.

---

## Features

- **User Authentication**: Sign up, log in, log out, and profile editing powered by [Devise](https://github.com/heartcombo/devise) (`before_action :authenticate_user!` enforced across the app).
- **User Avatars**: Automatic Gravatar profile image integration via [Gravtastic](https://github.com/chrislloyd/gravtastic).
- **Idea Management (CRUD)**:
  - Create, view, update, and delete ideas with a name, description, and picture.
  - Responsive 3-column grid layout on the Ideas index page using Bootstrap.
- **Image Uploads & Resizing**:
  - File uploads handled via [CarrierWave](https://github.com/carrierwaveuploader/carrierwave).
  - Automatic `50x50` thumbnail generation (`:thumb` version) using [MiniMagick](https://github.com/minimagick/minimagick) (ImageMagick).
- **Comments System**: Full CRUD support for comments associated with individual ideas (`Idea` `has_many :comments`).
- **Static Info Page**: Includes an informational page (`/pages/info`) introducing *Shop on Sale*.
- **JSON API Support**: Jbuilder templates included for `ideas` and `comments` (`index` and `show` endpoints).

---

## Tech Stack

| Component | Technology |
| :--- | :--- |
| **Framework** | Ruby on Rails `4.2.0` |
| **Database** | SQLite3 |
| **Authentication** | Devise |
| **Image Uploading & Processing** | CarrierWave + MiniMagick (`3.8.0`) |
| **Avatars** | Gravtastic |
| **Frontend / Styling** | Bootstrap 3, SCSS (`sass-rails`), CoffeeScript, jQuery, Turbolinks |

---

## Prerequisites

Before setting up the project locally, make sure you have the following installed:

- **Ruby** (compatible with Rails 4.2, e.g., Ruby `2.1` – `2.3`)
- **Bundler** (`gem install bundler`)
- **SQLite3**
- **ImageMagick** (required by `mini_magick` for image resizing)
  - macOS: `brew install imagemagick`
  - Ubuntu/Debian: `sudo apt-get install imagemagick`

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/zainmasri/rails-girls.git
cd rails-girls
```

### 2. Install dependencies

```bash
bundle install
```

### 3. Set up the database

Run the migrations to create the `ideas`, `comments`, and `users` tables in SQLite:

```bash
bin/rake db:migrate
```

*(Optional)* You can also use the included setup script to install dependencies, load the schema, and clean logs/tempfiles:

```bash
bin/setup
```

### 4. Start the development server

```bash
bin/rails server
```

Open your browser and navigate to [http://localhost:3000](http://localhost:3000). You will be prompted to sign up or log in before viewing `/ideas`.

---

## Application Routes

| Route | HTTP Verb | Controller#Action | Description |
| :--- | :--- | :--- | :--- |
| `/` | `GET` | Redirects to `/ideas` | Root path |
| `/ideas` | `GET`, `POST` | `ideas#index`, `ideas#create` | List all ideas / Create a new idea |
| `/ideas/new` | `GET` | `ideas#new` | Form to create a new idea |
| `/ideas/:id` | `GET`, `PATCH`, `DELETE` | `ideas#show`, `ideas#update`, `ideas#destroy` | View, update, or delete an idea |
| `/ideas/:id/edit` | `GET` | `ideas#edit` | Form to edit an existing idea |
| `/comments` | `GET`, `POST`, etc. | `comments#*` | RESTful routes for idea comments |
| `/pages/info` | `GET` | `pages#info` | Static info page |
| `/users/*` | `GET`, `POST`, `DELETE` | `devise/*` | User registration, login, logout, and password recovery |

---

## Database Schema Overview

- **`users`**: Managed by Devise (`email`, `encrypted_password`, `sign_in_count`, reset tokens, timestamps).
- **`ideas`**: Stores `name` (`string`), `description` (`text`), `picture` (`string`), and timestamps.
- **`comments`**: Stores `user_name` (`string`), `body` (`text`), `idea_id` (`integer` foreign key), and timestamps.

---

## Running Tests

To run the Minitest test suite for models and controllers:

```bash
bin/rake test
```
