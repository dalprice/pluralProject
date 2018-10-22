# Import Script

-- phpMyAdmin SQL Dump
-- version 4.8.3
-- https://www.phpmyadmin.net/
--
-- Host: localhost:8889
-- Generation Time: Oct 20, 2018 at 07:05 PM
-- Server version: 5.7.23
-- PHP Version: 7.2.8

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";

--
-- Database: `pluralprojectfinal`
--
CREATE DATABASE IF NOT EXISTS `pluralprojectfinal` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
USE `pluralprojectfinal`;

DELIMITER $$
--
-- Procedures
--
CREATE DEFINER=`root`@`localhost` PROCEDURE `get_author_consultant` (IN `getauthor` INT(11))  BEGIN
SELECT users.name AS author_name, employee.employee_id, employee.FirstName, employee.LastName, subjectexpert.subject_expert_type FROM users
JOIN author ON users.user_id = author.author_type
JOIN pluralconsultant ON author.pluralconsultant_No = pluralconsultant.PLURALCONSULTANT_No
JOIN subjectexpert ON subjectexpert.PLURALCONSULTANT_No = pluralconsultant.PLURALCONSULTANT_No
JOIN employee ON pluralconsultant.employee_id = employee.employee_id
WHERE author.author_type = getauthor;
END$$

CREATE DEFINER=`root`@`localhost` PROCEDURE `show_course_by_path` (IN `getpath` INT(11))  BEGIN
SELECT course.* FROM course
JOIN path ON path.path_id = course.path_id
WHERE path.path_id = getpath;
END$$

DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `author`
--

CREATE TABLE `author` (
  `author_type` int(11) NOT NULL,
  `website` varchar(50) DEFAULT NULL,
  `pluralconsultant_No` int(11) DEFAULT NULL,
  `mediamanager_No` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `author`
--

INSERT INTO `author` (`author_type`, `website`, `pluralconsultant_No`, `mediamanager_No`) VALUES
(1, 'www.JohnBarrowman.com', 104, 212),
(2, 'www.AlexBorg.com', 101, 213),
(3, 'www.DanielChris.com', 103, 215),
(4, 'www.MaryDoll.com', 102, 214);

-- --------------------------------------------------------

--
-- Table structure for table `card`
--

CREATE TABLE `card` (
  `cc_number` bigint(16) NOT NULL,
  `student_type` int(11) NOT NULL,
  `expiration` date NOT NULL,
  `CVV` int(5) NOT NULL,
  `type` varchar(25) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `card`
--

INSERT INTO `card` (`cc_number`, `student_type`, `expiration`, `CVV`, `type`) VALUES
(144724139775610, 8, '2023-05-15', 8626, 'American Express'),
(168672976697326, 2, '2022-01-08', 3216, 'American Express'),
(798096978476297, 20, '2024-12-15', 7248, 'American Express'),
(851685041183892, 1, '2020-05-06', 623, 'Visa'),
(1142365484181227, 12, '2020-03-28', 949, 'MasterCard'),
(1945435289484899, 15, '2019-10-15', 719, 'Visa'),
(2724812008985416, 17, '2021-11-06', 612, 'Visa'),
(3197580340246149, 18, '2022-02-26', 341, 'Visa'),
(4167749972612088, 6, '2018-02-14', 636, 'Visa'),
(4446142642103794, 4, '2019-05-25', 325, 'MasterCard'),
(5288531758643044, 9, '2022-08-10', 945, 'Visa'),
(5392693003463617, 19, '2023-10-26', 62, 'MasterCard'),
(6883546435828929, 11, '2022-01-20', 725, 'Visa'),
(7055083718406863, 3, '2019-03-22', 235, 'Visa'),
(7277646451075998, 10, '2025-11-06', 623, 'Visa'),
(7400345312708917, 5, '2026-03-19', 862, 'Visa'),
(7873228456592487, 14, '2020-08-16', 914, 'MasterCard'),
(8216534637938384, 7, '2021-02-06', 264, 'Visa'),
(8754996340594690, 16, '2020-08-19', 340, 'Visa'),
(9117972279541154, 13, '2017-06-27', 268, 'Visa');

-- --------------------------------------------------------

--
-- Table structure for table `certification`
--

CREATE TABLE `certification` (
  `author_type` int(11) NOT NULL,
  `certification_type` varchar(25) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `certification`
--

INSERT INTO `certification` (`author_type`, `certification_type`) VALUES
(1, 'database'),
(2, 'java'),
(3, 'servers'),
(4, 'big_data');

-- --------------------------------------------------------

--
-- Table structure for table `comment`
--

CREATE TABLE `comment` (
  `comment_id` int(11) NOT NULL,
  `text` varchar(110) DEFAULT NULL,
  `enrollment_id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `comment`
--

INSERT INTO `comment` (`comment_id`, `text`, `enrollment_id`) VALUES
(1, 'So Impressed with the course', 1),
(2, 'Course is useful, thats about it', 2),
(3, '10 times better then previuos course.', 3),
(4, 'So Impressed with the course', 4),
(5, 'The speakers are fantastic.', 5),
(6, 'This is an excellent', 6),
(7, 'So good with the course', 7),
(8, 'Teachers are good.', 8),
(9, 'So Impressed with the course', 9),
(10, 'Course is useful, thats about it', 10),
(11, 'So good with the course', 11),
(12, 'Teachers are good.', 12),
(13, 'So Impressed with the course', 13),
(14, '10 times better then previuos course', 14),
(15, 'So Impressed with the course', 15),
(16, 'The speakers are fantastic.', 16),
(17, 'Teachers are good.', 17),
(18, 'This is excellent', 18),
(19, 'This is excellent', 19),
(20, 'So Impressed with the course', 20);

-- --------------------------------------------------------

--
-- Table structure for table `company`
--

CREATE TABLE `company` (
  `company_id` int(11) NOT NULL,
  `name` varchar(50) NOT NULL,
  `employee_count` int(11) DEFAULT NULL,
  `industry` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `company`
--

INSERT INTO `company` (`company_id`, `name`, `employee_count`, `industry`) VALUES
(1, 'Deluge Enterprises', 3000, 'Retail'),
(2, 'Nymph Co.', 200, 'Energy'),
(3, 'Electra Sports', 500, 'Entertainment'),
(4, 'Phenomenologies', 8000, 'Health Care'),
(5, 'Luckytronics', 1500, 'Computer'),
(6, 'Electrorks', 6200, 'Energy'),
(7, 'Dragonetworks', 120, 'Computer'),
(8, 'Fairywater', 60, 'Food'),
(9, 'Tigerbite', 500, 'Defense'),
(10, 'Blueworth', 500, 'Agriculture'),
(11, 'Thor Acoustics', 100, 'Entertainment'),
(12, 'Blizzard Arts', 1200, 'Entertainment'),
(13, 'Cavern Industries', 3500, 'Mining'),
(14, 'Sawwares', 400, 'Computer'),
(15, 'Mountelligence', 350, 'Information'),
(16, 'Antelligence', 2000, 'Information'),
(17, 'Signway', 5600, 'Construction'),
(18, 'Zeusways', 40, 'Computer'),
(19, 'Betaways', 450, 'Computer'),
(20, 'Plutronics', 90, 'Computer');

-- --------------------------------------------------------

--
-- Table structure for table `course`
--

CREATE TABLE `course` (
  `course_name` varchar(50) NOT NULL,
  `course_id` int(11) NOT NULL,
  `description` varchar(50) DEFAULT NULL,
  `excercise_file` varchar(50) DEFAULT NULL,
  `author_name` varchar(50) NOT NULL,
  `publish_date` date DEFAULT NULL,
  `difficulty` varchar(50) DEFAULT NULL,
  `course_duration` float DEFAULT NULL,
  `course_rating` int(11) DEFAULT NULL,
  `path_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `course`
--

INSERT INTO `course` (`course_name`, `course_id`, `description`, `excercise_file`, `author_name`, `publish_date`, `difficulty`, `course_duration`, `course_rating`, `path_id`) VALUES
('Intro to SQL', 1, 'Basic SQL Queries', '101.sql', 'John Barrowman', '2017-11-15', 'Beginning', 3.5, 8, 11111),
('Advanced SQL', 2, 'Advanced Unions and Joins', '102.sql', 'John Barrowman', '2018-10-15', 'Advanced', 4, 9, 11111),
('NoSQL', 3, 'Basic NoSQL concepts', '105.sql', 'John Barrowman', '2016-08-17', 'Advanced', 2.25, 9, 11111),
('Database Management', 4, 'database administration', '200.sql', 'Mary Doll', '2018-02-15', 'Advanced', 4, 8, 11111),
('Intro to Python', 5, 'Python Basics', 'python.pdf', 'Alex Borg', '2018-04-15', 'Beginning', 4, 9, 22222),
('Advanced Python', 6, 'Advanced Python Applications', 'data.pdf', 'Alex Borg', '2018-08-20', 'Advanced', 5, 7, 22222),
('Intro to Javascript', 7, 'Javascript Fundamentals', 'practice.html', 'Alex Borg', '2014-02-25', 'Beginning', 4, 7, 22222),
('Advanced Javascript', 8, 'Javascript Advanced Applications', 'Website.html', 'Alex Borg', '2015-03-15', 'Advanced', 6.5, 8, 22222),
('Intro to Data Science ', 9, 'Data Science Fundamentals', 'practice.xls', 'Daniel Chris', '2016-12-15', 'Beginning', 4.5, 9, 22222),
('Intro to R', 10, 'Programming Language R', 'R1.html', 'Daniel Chris', '2018-09-15', 'Beginning', 5, 7, 22222),
('Advanced R', 11, 'Advanced R Applications', 'R2.html', 'Daniel Chris', '2018-10-01', 'Advanced', 4.25, 7, 22222),
('Into to Excel', 12, 'Excel Fundamentals', 'start.xls', 'Daniel Chris', '2018-05-15', 'Beginning', 6, 8, 33333),
('Intermediate Excel', 13, 'Excel functions and shortcuts', '2.xls', 'Mary Doll', '2016-12-15', 'Intermediate', 3.5, 9, 33333),
('Advanced Excel', 14, 'Advanced Excel functions and VBA', 'VBA.xls', 'Mary Doll', '2017-12-15', 'Advanced', 7, 7, 33333),
('Excel for Entrepreneurs', 15, 'Application of Excel to entrepreneurs', 'model.xls', 'John Barrowman', '2018-07-15', 'Intermediate', 5, 9, 33333),
('Intro to HTML', 16, 'HTML fundamentals', 'beginner.html', 'Mary Doll', '2015-03-15', 'Beginning', 3.25, 8, 44444),
('Advanced HTML', 17, 'Advanced HTML Concepts', 'advanced.html', 'Mary Doll', '2018-10-15', 'Advanced', 3.75, 8, 44444),
('Beginning CSS', 18, 'CSS Fundamentals', 'practice.css', 'John Barrowman', '2017-11-15', 'Beginning', 4.5, 7, 44444),
('Advanced CSS', 19, 'Advanced Concepts', 'advancedcss.css', 'John Barrowman', '2018-06-15', 'Advanced', 3.5, 8, 44444),
('UI Web Design', 20, 'Application of CSS and HTML to web design', 'Starter.html', 'John Barrowman', '2018-04-15', 'Beginning', 3.5, 9, 44444);

-- --------------------------------------------------------

--
-- Table structure for table `employee`
--

CREATE TABLE `employee` (
  `employee_id` int(11) NOT NULL,
  `isActive` varchar(20) DEFAULT NULL,
  `FirstName` varchar(50) DEFAULT NULL,
  `LastName` varchar(50) DEFAULT NULL,
  `start_date` date DEFAULT NULL,
  `end_date` date DEFAULT NULL,
  `title` varchar(50) DEFAULT NULL,
  `employee_type` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `employee`
--

INSERT INTO `employee` (`employee_id`, `isActive`, `FirstName`, `LastName`, `start_date`, `end_date`, `title`, `employee_type`) VALUES
(1, 'YES', 'Tyler', 'Barry', '2017-08-01', '2018-09-02', 'yhn', 'Consultant'),
(2, 'YES', 'Dal', 'Price', '2018-07-01', NULL, 'iop', 'Media Manager'),
(3, 'YES', 'Canchao', 'Bai', '2017-05-01', NULL, 'plk', 'Consultant'),
(4, 'YES', 'Ankit', 'Soi', '2017-05-01', '2018-09-01', 'lkm', 'Media Manager'),
(5, 'YES', 'Megha', 'Clark', '2017-05-01', '2018-09-01', 'opl', 'Consultant'),
(6, 'YES', 'Nealesh', 'Kapoor', '2017-05-01', '2018-09-01', 'asx', 'Consultant'),
(7, 'YES', 'Samesk', 'Bai', '2017-05-01', '2018-09-01', 'edc', 'Consultant'),
(8, 'YES', 'Jon', 'Bai', '2017-05-01', '2018-09-01', 'qwe', 'Consultant'),
(9, 'YES', 'Chad', 'Ben', '2018-05-01', '2018-09-01', 'vfr', 'Media Manager'),
(10, 'YES', 'Chuan', 'Jai', '2017-05-01', NULL, 'lmj', 'Consultant'),
(11, 'YES', 'Syn', 'Gup', '2017-05-01', '2018-09-01', 'edc', 'Consultant'),
(12, 'YES', 'Garry', 'Clark', '2017-05-01', '2018-09-01', 'saa', 'Media Manager'),
(13, 'YES', 'Kerry', 'Bai', '2017-05-01', '2018-09-01', 'klm', 'Consultant'),
(14, 'YES', 'Chedher', 'Rau', '2017-05-01', '2018-09-01', 'qwd', 'Media Manager'),
(15, 'YES', 'Milin', 'Bai', '2018-02-01', NULL, 'edc', 'Consultant'),
(16, 'YES', 'Fibi', 'Rai', '2017-05-01', '2018-09-01', 'wed', 'Media Manager'),
(17, 'YES', 'Kyona', 'Bai', '2017-05-01', '2018-09-01', 'kjh', 'Consultant'),
(18, 'YES', 'Shubhri', 'Bai', '2017-05-01', '2018-09-01', 'qwd', 'Media Manager'),
(19, 'YES', 'Suchita', 'Kapoor', '2017-05-01', '2018-09-01', 'rew', 'Consultant'),
(20, 'YES', 'Gaurav', 'Bhaiya', '2018-09-01', NULL, 'edc', 'Media Manager');

-- --------------------------------------------------------

--
-- Table structure for table `enrollment`
--

CREATE TABLE `enrollment` (
  `enrollment_id` int(11) NOT NULL,
  `start_time` date NOT NULL,
  `end_time` date NOT NULL,
  `completed_data` date NOT NULL,
  `bookmark` bit(1) DEFAULT NULL,
  `rating` varchar(5) DEFAULT NULL,
  `users_id` int(11) DEFAULT NULL,
  `course_id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `enrollment`
--

INSERT INTO `enrollment` (`enrollment_id`, `start_time`, `end_time`, `completed_data`, `bookmark`, `rating`, `users_id`, `course_id`) VALUES
(1, '2009-11-24', '2010-11-24', '2010-10-10', b'0', '4', 1, 6),
(2, '2008-11-24', '2009-11-24', '2009-10-10', b'0', '3', 2, 2),
(3, '2008-10-24', '2009-08-24', '2009-10-10', b'1', '4', 3, 4),
(4, '2008-10-24', '2009-10-24', '2009-10-10', b'0', '5', 2, 3),
(5, '2007-10-24', '2009-10-24', '2009-10-10', b'0', '4', 3, 6),
(6, '2007-10-24', '2008-10-24', '2009-10-10', b'1', '5', 4, 7),
(7, '2007-08-24', '2009-10-24', '2009-10-10', b'0', '4', 15, 10),
(8, '2008-03-24', '2009-12-24', '2009-10-10', b'1', '5', 2, 1),
(9, '2008-10-24', '2009-10-24', '2009-10-10', b'0', '4', 14, 2),
(10, '2010-10-24', '2011-10-24', '2011-10-10', b'0', '5', 16, 3),
(11, '2010-11-18', '2011-10-24', '2011-10-10', b'0', '5', 2, 6),
(12, '2010-10-24', '2011-10-24', '2011-10-10', b'1', '4', 14, 8),
(13, '2011-05-24', '2012-04-24', '2012-10-10', b'0', '4', 15, 6),
(14, '2010-10-22', '2011-10-24', '2011-10-10', b'0', '15', 2, 7),
(15, '2015-09-24', '2016-08-24', '2016-10-10', b'1', '4', 12, 12),
(16, '2015-10-24', '2016-10-24', '2016-10-10', b'1', '5', 2, 7),
(17, '2015-07-11', '2016-09-24', '2015-10-10', b'1', '4', 2, 2),
(18, '2018-10-04', '2019-10-24', '2019-08-10', b'0', '5', 12, 6),
(19, '2018-10-30', '2019-10-24', '2019-08-10', b'1', '3', 13, 6),
(20, '2018-10-11', '2019-10-24', '2019-10-10', b'0', '4', 12, 6);

-- --------------------------------------------------------

--
-- Table structure for table `hobby`
--

CREATE TABLE `hobby` (
  `user_id` int(11) NOT NULL,
  `hobby` varchar(25) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `hobby`
--

INSERT INTO `hobby` (`user_id`, `hobby`) VALUES
(1, 'programming'),
(2, 'hiking'),
(3, 'reading'),
(4, 'programming'),
(5, 'hiking'),
(6, 'programming'),
(7, 'reading'),
(8, 'reading'),
(9, 'programming'),
(10, 'programming'),
(11, 'reading'),
(12, 'programming'),
(13, 'programming'),
(14, 'research'),
(15, 'programming'),
(16, 'programming'),
(17, 'programming'),
(18, 'researchg'),
(19, 'hiking'),
(20, 'hiking');

-- --------------------------------------------------------

--
-- Table structure for table `mediaexpert`
--

CREATE TABLE `mediaexpert` (
  `MEDIAMANAGER_No` int(11) NOT NULL,
  `media_expert_type` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `mediaexpert`
--

INSERT INTO `mediaexpert` (`MEDIAMANAGER_No`, `media_expert_type`) VALUES
(212, 'Adobe Premiere'),
(213, 'Final cut'),
(214, 'Adobe Premiere'),
(215, 'Final cut'),
(216, 'Adobe Premiere'),
(217, 'Final cut'),
(218, 'Adobe Premiere'),
(219, 'Final cut'),
(220, 'Adobe Premiere'),
(221, 'Final cut'),
(222, 'Adobe Premiere'),
(223, 'Final cut'),
(224, 'Adobe Premiere'),
(225, 'Final cut'),
(226, 'Adobe Premiere'),
(227, 'Final cut'),
(228, 'Adobe Premiere'),
(229, 'Final cut'),
(230, 'Adobe Premiere'),
(231, 'Final cut');

-- --------------------------------------------------------

--
-- Table structure for table `mediamanager`
--

CREATE TABLE `mediamanager` (
  `MEDIAMANAGER_No` int(11) NOT NULL,
  `employee_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `mediamanager`
--

INSERT INTO `mediamanager` (`MEDIAMANAGER_No`, `employee_id`) VALUES
(212, 1),
(213, 2),
(214, 3),
(215, 4),
(216, 5),
(217, 6),
(218, 7),
(219, 8),
(220, 9),
(221, 10),
(222, 11),
(223, 12),
(224, 13),
(225, 14),
(226, 15),
(227, 16),
(228, 17),
(229, 18),
(230, 19),
(231, 20);

-- --------------------------------------------------------

--
-- Stand-in structure for view `new_employees`
-- (See below for the actual view)
--
CREATE TABLE `new_employees` (
`employee_id` int(11)
,`isActive` varchar(20)
,`FirstName` varchar(50)
,`LastName` varchar(50)
,`start_date` date
,`end_date` date
,`title` varchar(50)
,`employee_type` varchar(50)
);

-- --------------------------------------------------------

--
-- Table structure for table `path`
--

CREATE TABLE `path` (
  `path_id` int(11) NOT NULL,
  `name` varchar(50) NOT NULL,
  `description` varchar(50) DEFAULT NULL,
  `certificate` varchar(50) DEFAULT NULL,
  `publish_date` date DEFAULT NULL,
  `career_path` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `path`
--

INSERT INTO `path` (`path_id`, `name`, `description`, `certificate`, `publish_date`, `career_path`) VALUES
(1111, 'IT Leadership', 'Another Path', 'Certificate', '2018-08-01', 'IT Leader'),
(11111, 'Database Management', 'SQL and Database Admin', 'Basic Database', '2018-10-01', 'Database'),
(11112, 'PHP', 'Another Path', 'Certificate', '2018-08-01', 'PHP'),
(11113, 'Adobe Photoshop', 'Another Path', 'Certificate', '2017-08-01', 'Photoshop'),
(11114, 'HTML', 'HTML for the workplace', 'Certificate', '2018-10-01', 'HTML Web'),
(11115, 'Adobe Premiere', 'Another Path', 'Premiere Essentials', '2018-08-01', 'Adobe Premiere'),
(11116, 'Coding', 'Another Path', 'Coding 201', '2018-08-01', 'Coding'),
(11117, 'WAMP', 'Another Path', 'WAMP 201', '2018-08-01', 'IS 6420'),
(11118, 'xAPI', 'Another Path', 'XAPI Learning', '2018-08-01', 'Instructional Designer'),
(11119, 'SCORM', 'Another Path', 'SCORM 1', '2018-08-01', 'LMS'),
(11120, 'Oracle', 'Oracle Database Systems', 'Oracle 201', '2018-09-01', 'Oracle Database'),
(22222, 'Data Analytics', 'Data and Businss Analytics', 'Basic Analytics', '2018-09-03', 'Analytics'),
(33333, 'Excel', 'Excel for IT professionals', 'Excel Path 1', '2017-12-01', 'Excel'),
(44444, 'Web Design', 'Basic Web Desgin', 'Web Design 101', '2018-04-01', 'Web Designer'),
(55555, 'Cyber Security', 'Basic Defensive Cyber Secuity', 'Security 101', '2018-07-01', 'Cyber Security'),
(66166, 'Python', 'Another Python Path', 'Basic', '2018-08-01', 'Python Engineer'),
(77777, 'Azure', 'Azure Basics', 'Basic', '2018-08-01', 'Azure Admin'),
(88888, 'C++', 'C++ for design', 'C++ 201', '2018-06-01', 'C++ Engineer'),
(99991, 'Endpoint Management', 'Another Path', 'Certificate', '2018-08-01', 'IT Professional'),
(99999, 'C#', 'C# for design', 'Certificate', '2018-08-01', 'C# Engineer');

-- --------------------------------------------------------

--
-- Table structure for table `payment`
--

CREATE TABLE `payment` (
  `student_type` int(11) NOT NULL,
  `subscription_id` int(11) NOT NULL,
  `payment_date` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `payment`
--

INSERT INTO `payment` (`student_type`, `subscription_id`, `payment_date`) VALUES
(1, 1, '2018-08-15'),
(2, 2, '2018-08-11'),
(3, 3, '2018-08-22'),
(4, 4, '2018-08-06'),
(5, 5, '2018-09-04'),
(6, 6, '2018-08-12'),
(7, 7, '2018-08-06'),
(8, 8, '2018-08-20'),
(9, 9, '2018-08-06'),
(10, 10, '2018-08-20'),
(11, 11, '2018-08-06'),
(12, 12, '2018-09-15'),
(13, 13, '2018-08-16'),
(14, 14, '2018-08-25'),
(15, 15, '2018-08-16'),
(16, 16, '2018-08-21'),
(17, 17, '2018-08-15'),
(18, 18, '2018-08-16'),
(19, 19, '2018-08-24'),
(20, 20, '2018-08-12');

-- --------------------------------------------------------

--
-- Table structure for table `pluralconsultant`
--

CREATE TABLE `pluralconsultant` (
  `PLURALCONSULTANT_No` int(11) NOT NULL,
  `employee_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `pluralconsultant`
--

INSERT INTO `pluralconsultant` (`PLURALCONSULTANT_No`, `employee_id`) VALUES
(101, 1),
(102, 2),
(103, 3),
(104, 4),
(105, 5),
(106, 6),
(107, 7),
(108, 8),
(109, 9),
(110, 10),
(111, 11),
(112, 12),
(113, 13),
(114, 14),
(115, 15),
(116, 16),
(117, 17),
(118, 18),
(119, 19),
(120, 20);

-- --------------------------------------------------------

--
-- Table structure for table `question`
--

CREATE TABLE `question` (
  `question_id` int(11) NOT NULL,
  `question` varchar(100) DEFAULT NULL,
  `answer` varchar(100) DEFAULT NULL,
  `incorrect_choice` varchar(100) DEFAULT NULL,
  `skilliq_id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `question`
--

INSERT INTO `question` (`question_id`, `question`, `answer`, `incorrect_choice`, `skilliq_id`) VALUES
(10, 'A ______ can have only one value', 'single value', 'composite Entity', 101),
(11, 'A ______ can have more than one value', 'composite entity', 'single value Entity', 101),
(12, 'A property or characteristic of an entity', 'attribute', 'value', 101),
(13, 'An attribute must be a noun', 'true', 'false', 101),
(14, 'Two attributes should not have the same name', 'true', 'false', 101),
(15, 'An indentifier attribute is like a _______', 'primary key', 'foreign key', 101),
(16, 'A student SSN is most likely a ', 'primary key', 'single value Entity', 101),
(17, 'SQL coding is most likely done in _______', 'database implementation', 'logical design', 101),
(18, 'A ______ brings together two tables', 'join', 'composite attribute', 101),
(19, 'A ______ brings together two querries', 'union', 'minus', 101),
(20, 'A left join ignores_______', 'null values on the right', 'the left table', 101),
(21, 'A right join ignores______', 'null values on the left', 'single value Entity', 101),
(22, 'A ____ is numeric data type', 'int', 'varchar', 101),
(23, 'Which is the correct date format', 'MM-DD-YYYY', 'M-D-Y', 101),
(24, 'A ______ saves you time coding', 'stored procedure', 'composite attribute', 101),
(25, 'A ____ is stored in your database', 'view', 'SQL', 101),
(26, '____ can store images', 'noSQL database', 'dropbox', 101),
(27, 'A ______ can have more than one value', 'composite entity', 'single value Entity', 101),
(28, 'Two attributes should not have the same name', 'true', 'false', 101),
(29, 'A ______ can have more than one value', 'composite entity', 'true entity', 101),
(30, 'A student SSN is most likely a ', 'primary key', 'single value Entity', 101);

-- --------------------------------------------------------

--
-- Table structure for table `recommended`
--

CREATE TABLE `recommended` (
  `original_course` int(11) NOT NULL,
  `recommended_course` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `recommended`
--

INSERT INTO `recommended` (`original_course`, `recommended_course`) VALUES
(20, 1),
(1, 2),
(2, 3),
(3, 4),
(4, 5),
(5, 6),
(6, 7),
(7, 8),
(12, 8),
(8, 9),
(10, 11),
(11, 12),
(13, 14),
(14, 15),
(15, 16),
(17, 18),
(18, 19),
(19, 20);

-- --------------------------------------------------------

--
-- Table structure for table `royalty`
--

CREATE TABLE `royalty` (
  `royalty_id` int(11) NOT NULL,
  `amount` float DEFAULT NULL,
  `type` varchar(50) DEFAULT NULL,
  `course_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `royalty`
--

INSERT INTO `royalty` (`royalty_id`, `amount`, `type`, `course_id`) VALUES
(1, 500, 'monthly', 1),
(2, 7000, 'yearly', 2),
(3, 600, 'monthly', 3),
(4, 7000, 'yearly', 4),
(5, 10000, 'yearly', 5),
(6, 700, 'monthly', 6),
(7, 700, 'monthly', 7),
(8, 500, 'monthly', 8),
(9, 600, 'monthly', 9),
(10, 500, 'monthly', 10),
(11, 8000, 'yearly', 11),
(12, 600, 'monthly', 12),
(13, 500, 'monthly', 13),
(14, 8000, 'yearly', 14),
(15, 7000, 'yearly', 15),
(16, 6000, 'yearly', 16),
(17, 500, 'monthly', 17),
(18, 8000, 'yearly', 18),
(19, 7000, 'yearly', 19),
(20, 500, 'monthly', 20);

-- --------------------------------------------------------

--
-- Table structure for table `royaltypayment`
--

CREATE TABLE `royaltypayment` (
  `royalty_id` int(11) NOT NULL,
  `course_id` int(11) NOT NULL,
  `royalty_date` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `royaltypayment`
--

INSERT INTO `royaltypayment` (`royalty_id`, `course_id`, `royalty_date`) VALUES
(1, 1, '2018-09-01'),
(2, 2, '2018-09-01'),
(3, 3, '2018-09-01'),
(4, 4, '2018-09-01'),
(5, 5, '2018-09-01'),
(6, 6, '2018-09-01'),
(7, 7, '2018-09-01'),
(8, 8, '2018-09-01'),
(9, 9, '2018-09-01'),
(10, 10, '2018-09-01'),
(11, 11, '2018-09-01'),
(12, 12, '2018-09-01'),
(13, 13, '2018-09-01'),
(14, 14, '2018-09-01'),
(15, 15, '2018-09-01'),
(16, 16, '2018-09-01'),
(17, 17, '2018-09-01'),
(18, 18, '2018-09-01'),
(19, 19, '2018-09-01'),
(20, 20, '2018-09-01');

-- --------------------------------------------------------

--
-- Table structure for table `score`
--

CREATE TABLE `score` (
  `skilliqID` int(11) NOT NULL,
  `student_type` int(11) NOT NULL,
  `student_score` int(5) DEFAULT NULL,
  `date_taken` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `score`
--

INSERT INTO `score` (`skilliqID`, `student_type`, `student_score`, `date_taken`) VALUES
(101, 1, 50, '2018-04-11'),
(102, 2, 75, '2017-09-01'),
(103, 3, 65, '2018-06-01'),
(104, 4, 80, '2016-05-01'),
(105, 5, 74, '2018-08-01'),
(106, 1, 99, '2017-12-01'),
(107, 2, 99, '2018-07-01'),
(108, 3, 55, '2018-07-01'),
(109, 4, 99, '2018-01-01'),
(110, 5, 70, '2018-05-01'),
(111, 6, 99, '2018-07-01'),
(112, 1, 79, '2018-06-01'),
(113, 2, 99, '2018-07-01'),
(114, 3, 50, '2018-10-01'),
(115, 4, 59, '2018-07-01'),
(116, 5, 100, '2017-11-01'),
(117, 6, 99, '2018-07-01'),
(118, 1, 99, '2018-07-01'),
(119, 2, 40, '2018-07-01'),
(120, 6, 99, '2018-07-01');

-- --------------------------------------------------------

--
-- Table structure for table `skilliq`
--

CREATE TABLE `skilliq` (
  `skilliq_id` int(11) NOT NULL,
  `name` varchar(50) NOT NULL,
  `test_date` date DEFAULT NULL,
  `path_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `skilliq`
--

INSERT INTO `skilliq` (`skilliq_id`, `name`, `test_date`, `path_id`) VALUES
(101, 'Path 1', '2018-04-11', 11111),
(102, 'Path 2', '2017-09-01', 22222),
(103, 'Path 3', '2018-06-01', 33333),
(104, 'Path 4', '2016-05-01', 44444),
(105, 'Path 1', '2018-08-01', 11111),
(106, 'Path 2', '2017-12-01', 22222),
(107, 'Path 3', '2018-07-01', 33333),
(108, 'Path 4', '2018-07-01', 44444),
(109, 'Path 1', '2018-01-01', 11111),
(110, 'Path 2', '2018-05-01', 22222),
(111, 'Path 3', '2018-07-01', 33333),
(112, 'Path 4', '2018-06-01', 44444),
(113, 'Path 1', '2018-07-01', 11111),
(114, 'Path 2', '2018-10-01', 22222),
(115, 'Path 1', '2018-07-01', 11111),
(116, 'Path 3', '2017-11-01', 33333),
(117, 'Path 1', '2018-07-01', 11111),
(118, 'Path 1', '2018-07-01', 11111),
(119, 'Path 2', '2018-07-01', 22222),
(120, 'Path 1', '2018-07-01', 11111);

-- --------------------------------------------------------

--
-- Table structure for table `student`
--

CREATE TABLE `student` (
  `student_type` int(11) NOT NULL,
  `interests` varchar(25) DEFAULT NULL,
  `payment_methoed` varchar(25) DEFAULT NULL,
  `company_id` int(11) NOT NULL,
  `skill_id` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `student`
--

INSERT INTO `student` (`student_type`, `interests`, `payment_methoed`, `company_id`, `skill_id`) VALUES
(1, 'database', 'credit_card', 1, 95),
(2, 'networking', 'credit_card', 2, 82),
(3, 'database', 'credit_card', 3, 96),
(4, 'java', 'credit_card', 4, 95),
(5, 'web_application', 'credit_card', 5, 65),
(6, 'database', 'credit_card', 7, 82),
(7, 'database', 'credit_card', 8, 97),
(8, 'business_intelligence', 'credit_card', 10, 100),
(9, 'database', 'credit_card', 11, 95),
(10, 'business_intelligence', 'credit_card', 14, 98),
(11, 'IT_sercurity', 'credit_card', 15, 94),
(12, 'IT_sercurity', 'credit_card', 16, 86),
(13, 'IT_sercurity', 'credit_card', 17, 75),
(14, 'business_intelligence', 'credit_card', 18, 81),
(15, 'database', 'credit_card', 15, 85),
(16, 'big_data', 'credit_card', 16, 97),
(17, 'big_data', 'credit_card', 17, 95),
(18, 'IT_sercurity', 'credit_card', 20, 89),
(19, 'business_intelligence', 'credit_card', 18, 99),
(20, 'database', 'credit_card', 12, 95);

-- --------------------------------------------------------

--
-- Stand-in structure for view `student_expired_cc`
-- (See below for the actual view)
--
CREATE TABLE `student_expired_cc` (
`name` varchar(25)
,`cc_number` bigint(16)
,`student_type` int(11)
);

-- --------------------------------------------------------

--
-- Table structure for table `subjectexpert`
--

CREATE TABLE `subjectexpert` (
  `PLURALCONSULTANT_No` int(11) NOT NULL,
  `subject_expert_type` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `subjectexpert`
--

INSERT INTO `subjectexpert` (`PLURALCONSULTANT_No`, `subject_expert_type`) VALUES
(101, 'Programming'),
(102, 'Database'),
(103, 'AI'),
(104, 'Machine learning'),
(105, 'Computer Networks'),
(106, 'Security'),
(107, 'Wireless'),
(108, 'Programming'),
(109, 'Machine learning'),
(110, 'Security'),
(111, 'Wireless'),
(112, 'Security'),
(113, 'AI'),
(114, 'Database'),
(115, 'Database'),
(116, 'Database'),
(117, 'Wireless'),
(118, 'AI'),
(119, 'Programming'),
(120, 'Machine learning');

-- --------------------------------------------------------

--
-- Table structure for table `subscription`
--

CREATE TABLE `subscription` (
  `subscription_id` int(11) NOT NULL,
  `amount` float NOT NULL,
  `start_date` date NOT NULL,
  `end_date` date DEFAULT NULL,
  `subscription_type` varchar(50) DEFAULT NULL,
  `student_type` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `subscription`
--

INSERT INTO `subscription` (`subscription_id`, `amount`, `start_date`, `end_date`, `subscription_type`, `student_type`) VALUES
(1, 10.99, '2017-06-15', NULL, 'Monthly Subscription', 1),
(2, 10.99, '2015-08-03', NULL, 'Monthly Subscription', 2),
(3, 119.99, '2012-02-01', NULL, 'Yearly Subscription', 3),
(4, 10.99, '2018-08-01', NULL, 'Monthly Subscription', 4),
(5, 10.99, '2018-05-18', '2018-09-18', 'Monthly Subscription', 5),
(6, 119.99, '2013-04-10', NULL, 'Yearly Subscription', 6),
(7, 10.99, '2015-01-20', NULL, 'Monthly Subscription', 7),
(8, 10.99, '2010-11-08', NULL, 'Monthly Subscription', 8),
(9, 10.99, '2012-10-01', NULL, 'Monthly Subscription', 9),
(10, 10.99, '2017-07-01', NULL, 'Monthly Subscription', 10),
(11, 10.99, '2016-03-01', NULL, 'Monthly Subscription', 11),
(12, 119.99, '2014-03-01', '2015-02-28', 'Yearly Subscription', 12),
(13, 10.99, '2018-08-01', NULL, 'Monthly Subscription', 13),
(14, 10.99, '2016-12-01', NULL, 'Monthly Subscription', 14),
(15, 10.99, '2016-02-22', '2018-05-22', 'Monthly Subscription', 15),
(16, 119.99, '2015-04-01', NULL, 'Yearly Subscription', 16),
(17, 10.99, '2016-12-10', NULL, 'Monthly Subscription', 17),
(18, 10.99, '2018-01-01', '2018-03-01', 'Monthly Subscription', 18),
(19, 10.99, '2014-03-16', NULL, 'Monthly Subscription', 19),
(20, 10.99, '2018-04-20', NULL, 'Monthly Subscription', 20);

-- --------------------------------------------------------

--
-- Table structure for table `users`
--

CREATE TABLE `users` (
  `user_id` int(11) NOT NULL,
  `job_title` varchar(25) DEFAULT NULL,
  `name` varchar(25) NOT NULL,
  `street` varchar(30) DEFAULT NULL,
  `city` varchar(20) DEFAULT NULL,
  `state` varchar(2) DEFAULT NULL,
  `zipcode` varchar(5) DEFAULT NULL,
  `country` varchar(5) DEFAULT NULL,
  `student` bit(1) DEFAULT NULL,
  `author` bit(1) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `users`
--

INSERT INTO `users` (`user_id`, `job_title`, `name`, `street`, `city`, `state`, `zipcode`, `country`, `student`, `author`) VALUES
(1, 'student', 'John Doe', '200 Maple', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(2, 'student', 'Bill Doll', '300 West', 'SLC', 'UT', '84107', 'USA', b'1', b'0'),
(3, 'student', 'Josh Turburn', '250 North', 'SLC', 'UT', '84108', 'USA', b'1', b'0'),
(4, 'student', 'Mary Lee', '200 South', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(5, 'student', 'Jane Smith', '120 University', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(6, 'student', 'Luis Smith', '200 Maple', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(7, 'student', 'Ben Brown', '300 West', 'SLC', 'UT', '84107', 'USA', b'1', b'0'),
(8, 'student', 'Carl Smith', '250 North', 'SLC', 'UT', '84108', 'USA', b'1', b'0'),
(9, 'student', 'John Doll', '200 South', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(10, 'student', 'Jennet Chris', '120 University', 'SLC', 'UT', '84102', 'USA', b'1', b'0'),
(11, 'student', 'Joyce French', '200 Main', 'Tucson', 'AZ', '45102', 'USA', b'1', b'0'),
(12, 'student', 'Jennifer English', '250 State', 'Tucson', 'AZ', '45112', 'USA', b'1', b'0'),
(13, 'student', 'Tom Borg', '3000 Sunset', 'LA', 'CA', '12112', 'USA', b'1', b'0'),
(14, 'student', 'Helen Thomas', '1200 Hollywood', 'LA', 'CA', '12117', 'USA', b'1', b'0'),
(15, 'student', 'Brian Borg', '100 College', 'SF', 'CA', '17118', 'USA', b'1', b'0'),
(16, 'student', 'Keanu Reeves', '200 College', 'SF', 'CA', '17120', 'USA', b'1', b'0'),
(17, 'professor', 'John Barrowman', '300 College', 'SF', 'CA', '17130', 'USA', b'0', b'1'),
(18, 'professor', 'Alex Borg', '182 Main', 'SF', 'CA', '17118', 'USA', b'0', b'1'),
(19, 'professor', 'Daniel Chris', '700 South', 'SLC', 'UT', '84198', 'USA', b'0', b'1'),
(20, 'professor', 'Mary Doll', '1400 Hollywood', 'LA', 'CA', '12180', 'USA', b'1', b'1');

-- --------------------------------------------------------

--
-- Table structure for table `video`
--

CREATE TABLE `video` (
  `video_id` int(11) NOT NULL,
  `course_id` int(11) NOT NULL,
  `video_name` varchar(50) NOT NULL,
  `format` varchar(20) NOT NULL,
  `video_duration` time DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `video`
--

INSERT INTO `video` (`video_id`, `course_id`, `video_name`, `format`, `video_duration`) VALUES
(1, 1, 'Intro to SQL 1', 'MP4', '00:11:12'),
(2, 1, 'Intro to SQL 2', 'MP4', '00:05:30'),
(3, 1, 'Intro to SQL 3', 'MP4', '00:02:45'),
(4, 2, 'Advanced SQL 1', 'FLV', '00:06:32'),
(5, 2, 'Advanced SQL 2', 'RM', '00:08:22'),
(6, 3, 'Intro to NoSQL', 'WMV', '00:25:12'),
(7, 4, 'Intro to Database Management', 'MP4', '00:36:18'),
(8, 5, 'Intro to Python', 'MP4', '00:42:11'),
(9, 6, 'Advanced Python', 'MP4', '00:22:14'),
(10, 7, 'Intro to Javascript', 'RM', '00:53:36'),
(11, 8, 'Advanced Javascript', 'RM', '00:41:18'),
(12, 9, 'Intro to Data Science', 'WMV', '00:35:16'),
(13, 10, 'Intro to R', 'MP4', '00:13:12'),
(14, 11, 'Advanced R', 'MP4', '00:26:30'),
(15, 12, 'Intro to Excel 1', 'MP4', '00:08:45'),
(16, 12, 'Intro to Excel 2', 'FLV', '00:15:32'),
(17, 13, 'Intermediate Excel', 'RM', '00:08:22'),
(18, 14, 'Advanced Excel', 'WMV', '00:25:12'),
(19, 15, 'Excel for Entrepreneurs 1', 'MP4', '00:36:35'),
(20, 15, 'Excel for Entrepreneurs 2', 'MP4', '01:12:16'),
(21, 16, 'Intro to HTML', 'MP4', '00:28:18'),
(22, 17, 'Advanced HTML', 'RM', '00:33:26'),
(23, 18, 'Beginning CSS', 'RM', '00:51:14'),
(24, 19, 'Advanced CSS', 'WMV', '00:29:24'),
(25, 20, 'UI Web Design', 'WMV', '02:35:16');

-- --------------------------------------------------------

--
-- Structure for view `new_employees`
--
DROP TABLE IF EXISTS `new_employees`;

CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL SECURITY DEFINER VIEW `new_employees`  AS  select `employee`.`employee_id` AS `employee_id`,`employee`.`isActive` AS `isActive`,`employee`.`FirstName` AS `FirstName`,`employee`.`LastName` AS `LastName`,`employee`.`start_date` AS `start_date`,`employee`.`end_date` AS `end_date`,`employee`.`title` AS `title`,`employee`.`employee_type` AS `employee_type` from `employee` where (`employee`.`start_date` > '2018-01-01') ;

-- --------------------------------------------------------

--
-- Structure for view `student_expired_cc`
--
DROP TABLE IF EXISTS `student_expired_cc`;

CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL SECURITY DEFINER VIEW `student_expired_cc`  AS  select `users`.`name` AS `name`,`card`.`cc_number` AS `cc_number`,`student`.`student_type` AS `student_type` from ((`card` join `student` on((`card`.`student_type` = `student`.`student_type`))) join `users` on((`users`.`user_id` = `student`.`student_type`))) where (`card`.`expiration` < curdate()) ;

--
-- Indexes for dumped tables
--

--
-- Indexes for table `author`
--
ALTER TABLE `author`
  ADD PRIMARY KEY (`author_type`),
  ADD KEY `author_fk1` (`pluralconsultant_No`),
  ADD KEY `author_fk2` (`mediamanager_No`);

--
-- Indexes for table `card`
--
ALTER TABLE `card`
  ADD PRIMARY KEY (`cc_number`),
  ADD KEY `card_fk` (`student_type`);

--
-- Indexes for table `certification`
--
ALTER TABLE `certification`
  ADD PRIMARY KEY (`author_type`);

--
-- Indexes for table `comment`
--
ALTER TABLE `comment`
  ADD PRIMARY KEY (`comment_id`),
  ADD KEY `comment_fk1` (`enrollment_id`);

--
-- Indexes for table `company`
--
ALTER TABLE `company`
  ADD PRIMARY KEY (`company_id`);

--
-- Indexes for table `course`
--
ALTER TABLE `course`
  ADD PRIMARY KEY (`course_id`),
  ADD KEY `course_fk2` (`path_id`);

--
-- Indexes for table `employee`
--
ALTER TABLE `employee`
  ADD PRIMARY KEY (`employee_id`);

--
-- Indexes for table `enrollment`
--
ALTER TABLE `enrollment`
  ADD PRIMARY KEY (`enrollment_id`);

--
-- Indexes for table `hobby`
--
ALTER TABLE `hobby`
  ADD PRIMARY KEY (`user_id`);

--
-- Indexes for table `mediaexpert`
--
ALTER TABLE `mediaexpert`
  ADD PRIMARY KEY (`MEDIAMANAGER_No`);

--
-- Indexes for table `mediamanager`
--
ALTER TABLE `mediamanager`
  ADD PRIMARY KEY (`MEDIAMANAGER_No`),
  ADD KEY `mediamanager_fk` (`employee_id`);

--
-- Indexes for table `path`
--
ALTER TABLE `path`
  ADD PRIMARY KEY (`path_id`);

--
-- Indexes for table `payment`
--
ALTER TABLE `payment`
  ADD PRIMARY KEY (`student_type`,`subscription_id`),
  ADD KEY `payment_fk2` (`subscription_id`);

--
-- Indexes for table `pluralconsultant`
--
ALTER TABLE `pluralconsultant`
  ADD PRIMARY KEY (`PLURALCONSULTANT_No`),
  ADD KEY `pluralconsultant_fk` (`employee_id`);

--
-- Indexes for table `question`
--
ALTER TABLE `question`
  ADD PRIMARY KEY (`question_id`),
  ADD KEY `question_fk1` (`skilliq_id`);

--
-- Indexes for table `recommended`
--
ALTER TABLE `recommended`
  ADD PRIMARY KEY (`original_course`,`recommended_course`),
  ADD KEY `score_fk2` (`recommended_course`);

--
-- Indexes for table `royalty`
--
ALTER TABLE `royalty`
  ADD PRIMARY KEY (`royalty_id`),
  ADD KEY `royalty_fk1` (`course_id`);

--
-- Indexes for table `royaltypayment`
--
ALTER TABLE `royaltypayment`
  ADD PRIMARY KEY (`royalty_id`,`course_id`),
  ADD KEY `royaltypayment_fk2` (`course_id`);

--
-- Indexes for table `score`
--
ALTER TABLE `score`
  ADD PRIMARY KEY (`skilliqID`,`student_type`) USING BTREE,
  ADD KEY `score_fk4` (`student_type`);

--
-- Indexes for table `skilliq`
--
ALTER TABLE `skilliq`
  ADD PRIMARY KEY (`skilliq_id`),
  ADD KEY `skilliq_fk1` (`path_id`);

--
-- Indexes for table `student`
--
ALTER TABLE `student`
  ADD PRIMARY KEY (`student_type`),
  ADD KEY `student_fk1` (`company_id`);

--
-- Indexes for table `subjectexpert`
--
ALTER TABLE `subjectexpert`
  ADD PRIMARY KEY (`PLURALCONSULTANT_No`);

--
-- Indexes for table `subscription`
--
ALTER TABLE `subscription`
  ADD PRIMARY KEY (`subscription_id`);

--
-- Indexes for table `users`
--
ALTER TABLE `users`
  ADD PRIMARY KEY (`user_id`);

--
-- Indexes for table `video`
--
ALTER TABLE `video`
  ADD PRIMARY KEY (`video_id`),
  ADD KEY `video_fk` (`course_id`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `author`
--
ALTER TABLE `author`
  MODIFY `author_type` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;

--
-- AUTO_INCREMENT for table `certification`
--
ALTER TABLE `certification`
  MODIFY `author_type` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;

--
-- AUTO_INCREMENT for table `comment`
--
ALTER TABLE `comment`
  MODIFY `comment_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `company`
--
ALTER TABLE `company`
  MODIFY `company_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `employee`
--
ALTER TABLE `employee`
  MODIFY `employee_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `enrollment`
--
ALTER TABLE `enrollment`
  MODIFY `enrollment_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `hobby`
--
ALTER TABLE `hobby`
  MODIFY `user_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `royalty`
--
ALTER TABLE `royalty`
  MODIFY `royalty_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `student`
--
ALTER TABLE `student`
  MODIFY `student_type` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `subscription`
--
ALTER TABLE `subscription`
  MODIFY `subscription_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `users`
--
ALTER TABLE `users`
  MODIFY `user_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=21;

--
-- AUTO_INCREMENT for table `video`
--
ALTER TABLE `video`
  MODIFY `video_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=26;

--
-- Constraints for dumped tables
--

--
-- Constraints for table `author`
--
ALTER TABLE `author`
  ADD CONSTRAINT `author_fk1` FOREIGN KEY (`pluralconsultant_No`) REFERENCES `PLURALCONSULTANT` (`PLURALCONSULTANT_No`) ON UPDATE CASCADE,
  ADD CONSTRAINT `author_fk2` FOREIGN KEY (`mediamanager_No`) REFERENCES `MEDIAMANAGER` (`MEDIAMANAGER_No`) ON UPDATE CASCADE,
  ADD CONSTRAINT `author_fk3` FOREIGN KEY (`author_type`) REFERENCES `users` (`user_id`);

--
-- Constraints for table `card`
--
ALTER TABLE `card`
  ADD CONSTRAINT `card_fk` FOREIGN KEY (`student_type`) REFERENCES `student` (`student_type`) ON UPDATE CASCADE;

--
-- Constraints for table `comment`
--
ALTER TABLE `comment`
  ADD CONSTRAINT `comment_fk1` FOREIGN KEY (`enrollment_id`) REFERENCES `enrollment` (`enrollment_id`) ON UPDATE CASCADE;

--
-- Constraints for table `course`
--
ALTER TABLE `course`
  ADD CONSTRAINT `course_fk2` FOREIGN KEY (`path_id`) REFERENCES `path` (`path_id`) ON UPDATE CASCADE;

--
-- Constraints for table `mediaexpert`
--
ALTER TABLE `mediaexpert`
  ADD CONSTRAINT `mediaexpert_fk` FOREIGN KEY (`MEDIAMANAGER_No`) REFERENCES `mediamanager` (`MEDIAMANAGER_No`) ON UPDATE CASCADE;

--
-- Constraints for table `mediamanager`
--
ALTER TABLE `mediamanager`
  ADD CONSTRAINT `mediamanager_fk` FOREIGN KEY (`employee_id`) REFERENCES `employee` (`employee_id`) ON UPDATE CASCADE;

--
-- Constraints for table `payment`
--
ALTER TABLE `payment`
  ADD CONSTRAINT `payment_fk1` FOREIGN KEY (`student_type`) REFERENCES `student` (`student_type`) ON UPDATE CASCADE,
  ADD CONSTRAINT `payment_fk2` FOREIGN KEY (`subscription_id`) REFERENCES `subscription` (`subscription_id`) ON UPDATE CASCADE;

--
-- Constraints for table `pluralconsultant`
--
ALTER TABLE `pluralconsultant`
  ADD CONSTRAINT `pluralconsultant_fk` FOREIGN KEY (`employee_id`) REFERENCES `employee` (`employee_id`) ON UPDATE CASCADE;

--
-- Constraints for table `question`
--
ALTER TABLE `question`
  ADD CONSTRAINT `question_fk1` FOREIGN KEY (`skilliq_id`) REFERENCES `skilliq` (`skilliq_id`);

--
-- Constraints for table `recommended`
--
ALTER TABLE `recommended`
  ADD CONSTRAINT `score_fk1` FOREIGN KEY (`original_course`) REFERENCES `course` (`course_id`) ON UPDATE CASCADE,
  ADD CONSTRAINT `score_fk2` FOREIGN KEY (`recommended_course`) REFERENCES `course` (`course_id`) ON UPDATE CASCADE;

--
-- Constraints for table `royalty`
--
ALTER TABLE `royalty`
  ADD CONSTRAINT `royalty_fk1` FOREIGN KEY (`course_id`) REFERENCES `course` (`course_id`) ON UPDATE CASCADE;

--
-- Constraints for table `royaltypayment`
--
ALTER TABLE `royaltypayment`
  ADD CONSTRAINT `royaltypayment_fk1` FOREIGN KEY (`royalty_id`) REFERENCES `royalty` (`royalty_id`) ON UPDATE CASCADE,
  ADD CONSTRAINT `royaltypayment_fk2` FOREIGN KEY (`course_id`) REFERENCES `course` (`course_id`) ON UPDATE CASCADE;

--
-- Constraints for table `score`
--
ALTER TABLE `score`
  ADD CONSTRAINT `score_fk3` FOREIGN KEY (`skilliqID`) REFERENCES `skilliq` (`skilliq_id`) ON UPDATE CASCADE,
  ADD CONSTRAINT `score_fk4` FOREIGN KEY (`student_type`) REFERENCES `student` (`student_type`) ON UPDATE CASCADE;

--
-- Constraints for table `skilliq`
--
ALTER TABLE `skilliq`
  ADD CONSTRAINT `skilliq_fk1` FOREIGN KEY (`path_id`) REFERENCES `path` (`path_id`);

--
-- Constraints for table `student`
--
ALTER TABLE `student`
  ADD CONSTRAINT `student_fk1` FOREIGN KEY (`company_id`) REFERENCES `company` (`company_id`) ON UPDATE CASCADE,
  ADD CONSTRAINT `student_fk4` FOREIGN KEY (`student_type`) REFERENCES `users` (`user_id`);

--
-- Constraints for table `subjectexpert`
--
ALTER TABLE `subjectexpert`
  ADD CONSTRAINT `subjectexpert_fk` FOREIGN KEY (`PLURALCONSULTANT_No`) REFERENCES `pluralconsultant` (`PLURALCONSULTANT_No`) ON UPDATE CASCADE;

--
-- Constraints for table `video`
--
ALTER TABLE `video`
  ADD CONSTRAINT `video_fk` FOREIGN KEY (`course_id`) REFERENCES `course` (`course_id`) ON UPDATE CASCADE;


--
-- SQL STATEMENTS
--

-- Courses with videos that extend beyond an hour
SELECT course_name, SEC_TO_TIME(SUM( HOUR( video.video_duration) ) ) AS hours_summed from course
JOIN video ON video.course_id = course.course_id
GROUP BY course.course_name
HAVING SEC_TO_TIME(SUM(HOUR(video.video_duration))) >= 1;

-- Show all courses grouped by author
SELECT author_name, course_name FROM course
ORDER BY author_name;

-- Show all students with a Skill IQ above 90 for any given path
SELECT users.name, student.student_type, path.name AS path_name, score.student_score from path
JOIN skilliq ON skilliq.path_id = path.path_id
JOIN score ON score.skilliqID = skilliq.skilliq_id
JOIN student ON student.student_type = score.student_type
JOIN users ON users.user_id = student.student_type
WHERE score.student_score > 90
ORDER BY path.name;

-- Show courses that each user is currently enrolled in
SELECT users.name, course.course_name, enrollment.enrollment_id FROM users
JOIN enrollment ON enrollment.users_id=users.user_id
JOIN course ON course.course_id=enrollment.course_id ORDER BY users.user_id;

-- Show all course comments
SELECT course.course_id, course.course_name, users.name, text FROM comment
JOIN enrollment ON comment.enrollment_id = enrollment.enrollment_id
JOIN users ON enrollment.users_id = users.user_id
JOIN course ON enrollment.course_id = course.course_id;

--
-- VIEWS --
--

--  Show new employees View
--  CREATE VIEW new_employees AS
--  SELECT * FROM employee
--  WHERE start_date > "2018-01-01"

--  Show all credit cards that have expired View
--  CREATE VIEW student_expired_cc AS
--  SELECT cc_number, student.student_type FROM card
--  JOIN student ON card.student_type = student.student_type
--  WHERE expiration < CURRENT_DATE;

--
-- STORED PROCEDURES --
--

--  Show all courses in a path Sproc
--  DELIMITER //
--  CREATE PROCEDURE show_course_by_path (IN getpath int(11))
--  BEGIN
--  SELECT course.* FROM course
--  JOIN path ON path.path_id = course.path_id
--  WHERE path.path_id = getpath;
--  END //

--  DELIMITER //
--  CREATE PROCEDURE get_author_consultant (IN getauthor int(11))
--  BEGIN
--  SELECT users.name AS author_name, employee.employee_id, employee.FirstName, employee.LastName, subjectexpert.subject_expert_type FROM users
--  JOIN author ON users.user_id = author.author_type
--  JOIN pluralconsultant ON author.pluralconsultant_No = pluralconsultant.PLURALCONSULTANT_No
--  JOIN subjectexpert ON subjectexpert.PLURALCONSULTANT_No = pluralconsultant.PLURALCONSULTANT_No
--  JOIN employee ON pluralconsultant.employee_id = employee.employee_id
--  WHERE author.author_type = getauthor;
--  END //

