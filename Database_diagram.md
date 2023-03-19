# dbdiagram
```sql
CREATE TABLE articles
(
    id              serial primary key ,
    title           varchar(255) not null,
    slug            varchar(255) not null,
    body            text,
    description     varchar(255) not null,
    favorites_count int not null,
    user_id         int not null,
    created_at      date not null,
    updated_at      date not null
);

CREATE TABLE comments
(
    id          serial primary key,
    body        text not null,
    user_id     int  not null,
    articles_id int  not null,
    created_at  date not null,
    updated_at  date not null
);

CREATE TABLE favorites
(
    id          varchar(255) not null,
    user_id     int          not null,
    articles_id int          not null,
    created_at  date         not null,
    updated_at  date         not null
);

CREATE TABLE follows
(
    id              varchar(255) not null,
    followable_id   int          not null,
    followable_type varchar(255) not null,
    follower_id     int          not null,
    follower_type   varchar(255) not null,
    blocked         boolean,
    created_at      date         not null,
    updated_at      date         not null
);

CREATE TABLE taggings
(
    id            varchar(255) not null,
    tag_id        int          not null,
    taggable_id   int          not null,
    taggeble_type varchar(255) not null,
    tagger_id     int          not null,
    tagger_type   varchar(255) not null,
    context       varchar(255) not null,
    created_at    date         not null
);

CREATE TABLE tags
(
    id             varchar(255) not null,
    name           varchar(255) not null,
    taggongs_count int          not null,
);

CREATE TABLE users
(
    id                     varchar(255) not null,
    email                  varchar(255) not null,
    encrypted_password     varchar(255) not null,
    reset_password_token   varchar(255) not null,
    reset_password_sent_at date         not null,
    remember_created_at    date         not null,
    sign_in_count          int          not null,
    current_sign_in_at     date         not null,
    last_sign_in_at        date         not null,
    current_sign_in_up     varchar(255) not null,
    last_sign_in_up        varchar(255) not null,
    created_at             date         not null,
    updated_at             date         not null,
    username               varchar(255) not null,
    image                  varchar(255) not null,
    bio                    text         not null
);

ALTER TABLE users ADD CONSTRAINT fk_rails_articles_users FOREIGN KEY (id) REFERENCES articles (user_id);
ALTER TABLE users ADD CONSTRAINT fk_rails_comments_users FOREIGN KEY (id) REFERENCES comments (user_id);
ALTER TABLE articles ADD CONSTRAINT fk_rails_articles_articles FOREIGN KEY (id) REFERENCES comments (articles_id);
ALTER TABLE users ADD CONSTRAINT fk_rails_favorites_users FOREIGN KEY (id) REFERENCES favorites (user_id);
ALTER TABLE articles ADD CONSTRAINT fk_rails_favorites_articles FOREIGN KEY (id) REFERENCES favorites (articles_id);
ALTER TABLE tags ADD CONSTRAINT fk_rails_taggings_tags FOREIGN KEY (id) REFERENCES taggings (tag_id);
```
![Снимок экрана 2023-03-19 224048](https://user-images.githubusercontent.com/122611764/226197890-a6e5d113-60dc-4809-8ebe-fc6e1b9813bc.png)

