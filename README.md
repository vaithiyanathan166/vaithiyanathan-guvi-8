    TASK 8
using my sql  design a database whose name in imdb . create proper my sql tables ,primary key,foreign key,add data into the mysql tablesand do the following as given below ; 
1 ) movie should have multiple media (video or image)
2 ) movie can belongs to multiple genre
3 ) movie can have multiple reviews and review can belongs to a user
4) Artist can have multiple skills
5) Artist can perform multiple role in a single film

CREATE TABLE Movies (
    movie_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    release_year INT,
    description TEXT
);


INSERT INTO Movies (title, release_year, description)
VALUES ('Inception', 2010, 'A mind-bending thriller by Christopher Nolan.');

SELECT * FROM Movies;

 



CREATE TABLE Media (
    media_id INT AUTO_INCREMENT PRIMARY KEY,
    movie_id INT,
    media_type ENUM('image', 'video') NOT NULL,
    media_url VARCHAR(255) NOT NULL,
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id) ON DELETE CASCADE
);

INSERT INTO Media (movie_id, media_type, media_url)
VALUES (1, 'image', 'https://example.com/inception-image.jpg');

SELECT * FROM Media;

 ![image](https://github.com/user-attachments/assets/89d62490-d3c2-4888-973d-beaba3d2e4d9)


CREATE TABLE Genres (
    genre_id INT AUTO_INCREMENT PRIMARY KEY,
    genre_name VARCHAR(50) NOT NULL
);

INSERT INTO Genres (genre_name)
VALUES ('Sci-Fi'), ('Thriller');

SELECT * FROM Genres;
 
CREATE TABLE MovieGenres (
    movie_id INT,
    genre_id INT,
    PRIMARY KEY (movie_id, genre_id),
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id) ON DELETE CASCADE,
    FOREIGN KEY (genre_id) REFERENCES Genres(genre_id) ON DELETE CASCADE
);

INSERT INTO MovieGenres (movie_id, genre_id)
VALUES (1, 1), (1, 2);
SELECT * FROM MovieGenres;

 

CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE
);

INSERT INTO Users (username, email)
VALUES ('john_doe', 'john@example.com');

SELECT * FROM Users;

 
CREATE TABLE Reviews (
    review_id INT AUTO_INCREMENT PRIMARY KEY,
    movie_id INT,
    user_id INT,
    rating INT CHECK (rating >= 1 AND rating <= 10),
    review_text TEXT,
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE
);

INSERT INTO Reviews (movie_id, user_id, rating, review_text)
VALUES (1, 1, 9, 'Amazing movie with a great concept.');

SELECT * FROM Reviews;

 

CREATE TABLE Artists (
    artist_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    birth_date DATE
);

INSERT INTO Artists (name, birth_date)
VALUES ('Leonardo DiCaprio', '1974-11-11');

SELECT * FROM  Artists;
 

CREATE TABLE Skills (
    skill_id INT AUTO_INCREMENT PRIMARY KEY,
    skill_name VARCHAR(50) NOT NULL
);

INSERT INTO Skills (skill_name)
VALUES ('Acting'), ('Directing');

SELECT * FROM Skills;

 

CREATE TABLE ArtistSkills (
    artist_id INT,
    skill_id INT,
    PRIMARY KEY (artist_id, skill_id),
    FOREIGN KEY (artist_id) REFERENCES Artists(artist_id) ON DELETE CASCADE,
    FOREIGN KEY (skill_id) REFERENCES Skills(skill_id) ON DELETE CASCADE
);

INSERT INTO ArtistSkills (artist_id, skill_id)
VALUES (1, 1);

SELECT * FROM ArtistSkills;

 

CREATE TABLE Roles (
    role_id INT AUTO_INCREMENT PRIMARY KEY,
    role_name VARCHAR(50) NOT NULL
);

INSERT INTO Roles (role_name)
VALUES ('Actor'), ('Director');

SELECT * FROM Roles;

 

CREATE TABLE ArtistRoles (
    movie_id INT,
    artist_id INT,
    role_id INT,
    PRIMARY KEY (movie_id, artist_id, role_id),
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id) ON DELETE CASCADE,
    FOREIGN KEY (artist_id) REFERENCES Artists(artist_id) ON DELETE CASCADE,
    FOREIGN KEY (role_id) REFERENCES Roles(role_id) ON DELETE CASCADE
);

INSERT INTO ArtistRoles (movie_id, artist_id, role_id)
VALUES (1, 1, 1); 


SELECT * FROM ArtistRoles;


 
