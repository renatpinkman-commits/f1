-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Хост: 127.0.0.1
-- Время создания: Ноя 20 2026 г., 13:02
-- Версия сервера: 10.4.32-MariaDB
-- Версия PHP: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- База данных: `f1`
--

-- --------------------------------------------------------

--
-- Структура таблицы `drivers`
--

DROP TABLE IF EXISTS `drivers`;
CREATE TABLE `drivers` (
  `driver_id` varchar(20) NOT NULL,
  `driver_full_name` varchar(100) NOT NULL,
  `driver_number` int(11) NOT NULL,
  `team_id` varchar(20) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `drivers`
--

INSERT INTO `drivers` (`driver_id`, `driver_full_name`, `driver_number`, `team_id`) VALUES
('PILOT-001', 'Max Verstappen', 1, 'TEAM-02'),
('PILOT-016', 'Charles Leclerc', 16, 'TEAM-01');

-- --------------------------------------------------------

--
-- Структура таблицы `penalties`
--

DROP TABLE IF EXISTS `penalties`;
CREATE TABLE `penalties` (
  `driver_id` varchar(20) NOT NULL,
  `stage_id` varchar(30) NOT NULL,
  `violation_type` varchar(150) NOT NULL,
  `penalty_params` varchar(150) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `penalties`
--

INSERT INTO `penalties` (`driver_id`, `stage_id`, `violation_type`, `penalty_params`) VALUES
('PILOT-001', 'GP-2026-08', 'Speeding in pit lane', '5 sec'),
('PILOT-016', 'GP-2026-12', 'Track limits', '5 sec');

-- --------------------------------------------------------

--
-- Структура таблицы `session_results`
--

DROP TABLE IF EXISTS `session_results`;
CREATE TABLE `session_results` (
  `driver_id` varchar(20) NOT NULL,
  `stage_id` varchar(30) NOT NULL,
  `grid_position` int(11) NOT NULL,
  `finish_position` int(11) DEFAULT NULL,
  `finish_status` varchar(20) DEFAULT 'Finished',
  `points` decimal(4,1) DEFAULT 0.0,
  `fastest_lap` varchar(20) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `session_results`
--

INSERT INTO `session_results` (`driver_id`, `stage_id`, `grid_position`, `finish_position`, `finish_status`, `points`, `fastest_lap`) VALUES
('PILOT-001', 'GP-2026-08', 3, 2, 'Finished', 18.0, '00:01:14.512'),
('PILOT-016', 'GP-2026-08', 1, 1, 'Finished', 25.0, '00:01:14.260');

-- --------------------------------------------------------

--
-- Структура таблицы `stages`
--

DROP TABLE IF EXISTS `stages`;
CREATE TABLE `stages` (
  `stage_id` varchar(30) NOT NULL,
  `stage_name` varchar(100) NOT NULL,
  `track_id` varchar(20) NOT NULL,
  `session_date` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `stages`
--

INSERT INTO `stages` (`stage_id`, `stage_name`, `track_id`, `session_date`) VALUES
('GP-2026-08', 'Monaco Grand Prix', 'TRK-01', '2026-05-24'),
('GP-2026-12', 'British Grand Prix', 'TRK-02', '2026-07-05');

-- --------------------------------------------------------

--
-- Структура таблицы `teams`
--

DROP TABLE IF EXISTS `teams`;
CREATE TABLE `teams` (
  `team_id` varchar(20) NOT NULL,
  `team_name` varchar(100) NOT NULL,
  `country` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `teams`
--

INSERT INTO `teams` (`team_id`, `team_name`, `country`) VALUES
('TEAM-01', 'Scuderia Ferrari', 'Italy'),
('TEAM-02', 'Red Bull Racing', 'Austria');

-- --------------------------------------------------------

--
-- Структура таблицы `technical_components`
--

DROP TABLE IF EXISTS `technical_components`;
CREATE TABLE `technical_components` (
  `team_id` varchar(20) NOT NULL,
  `component_type` varchar(100) NOT NULL,
  `element_number` int(11) DEFAULT 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `technical_components`
--

INSERT INTO `technical_components` (`team_id`, `component_type`, `element_number`) VALUES
('TEAM-01', 'ICE', 2),
('TEAM-02', 'ICE', 3);

-- --------------------------------------------------------

--
-- Структура таблицы `tracks`
--

DROP TABLE IF EXISTS `tracks`;
CREATE TABLE `tracks` (
  `track_id` varchar(20) NOT NULL,
  `track_name` varchar(100) NOT NULL,
  `track_length` decimal(6,3) NOT NULL CHECK (`track_length` > 0)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Дамп данных таблицы `tracks`
--

INSERT INTO `tracks` (`track_id`, `track_name`, `track_length`) VALUES
('TRK-01', 'Circuit de Monaco', 3.337),
('TRK-02', 'Silverstone Circuit', 5.891);

-- --------------------------------------------------------

--
-- Дублирующая структура для представления `v_race_results`
-- (См. Ниже фактическое представление)
--
DROP VIEW IF EXISTS `v_race_results`;
CREATE TABLE `v_race_results` (
`driver_full_name` varchar(100)
,`team_name` varchar(100)
,`stage_id` varchar(30)
,`points` decimal(4,1)
);

-- --------------------------------------------------------

--
-- Структура для представления `v_race_results`
--
DROP TABLE IF EXISTS `v_race_results`;

DROP VIEW IF EXISTS `v_race_results`;
CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL SECURITY DEFINER VIEW `v_race_results`  AS SELECT `drivers`.`driver_full_name` AS `driver_full_name`, `teams`.`team_name` AS `team_name`, `session_results`.`stage_id` AS `stage_id`, `session_results`.`points` AS `points` FROM ((`session_results` join `drivers` on(`session_results`.`driver_id` = `drivers`.`driver_id`)) join `teams` on(`drivers`.`team_id` = `teams`.`team_id`)) ;

--
-- Индексы сохранённых таблиц
--

--
-- Индексы таблицы `drivers`
--
ALTER TABLE `drivers`
  ADD PRIMARY KEY (`driver_id`),
  ADD KEY `idx_drivers_team` (`team_id`);

--
-- Индексы таблицы `penalties`
--
ALTER TABLE `penalties`
  ADD PRIMARY KEY (`driver_id`,`stage_id`),
  ADD KEY `stage_id` (`stage_id`);

--
-- Индексы таблицы `session_results`
--
ALTER TABLE `session_results`
  ADD PRIMARY KEY (`driver_id`,`stage_id`),
  ADD KEY `stage_id` (`stage_id`);

--
-- Индексы таблицы `stages`
--
ALTER TABLE `stages`
  ADD PRIMARY KEY (`stage_id`),
  ADD KEY `track_id` (`track_id`);

--
-- Индексы таблицы `teams`
--
ALTER TABLE `teams`
  ADD PRIMARY KEY (`team_id`);

--
-- Индексы таблицы `technical_components`
--
ALTER TABLE `technical_components`
  ADD PRIMARY KEY (`team_id`,`component_type`);

--
-- Индексы таблицы `tracks`
--
ALTER TABLE `tracks`
  ADD PRIMARY KEY (`track_id`);

--
-- Ограничения внешнего ключа сохраненных таблиц
--

--
-- Ограничения внешнего ключа таблицы `drivers`
--
ALTER TABLE `drivers`
  ADD CONSTRAINT `drivers_ibfk_1` FOREIGN KEY (`team_id`) REFERENCES `teams` (`team_id`) ON DELETE CASCADE;

--
-- Ограничения внешнего ключа таблицы `penalties`
--
ALTER TABLE `penalties`
  ADD CONSTRAINT `penalties_ibfk_1` FOREIGN KEY (`driver_id`) REFERENCES `drivers` (`driver_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `penalties_ibfk_2` FOREIGN KEY (`stage_id`) REFERENCES `stages` (`stage_id`) ON DELETE CASCADE;

--
-- Ограничения внешнего ключа таблицы `session_results`
--
ALTER TABLE `session_results`
  ADD CONSTRAINT `session_results_ibfk_1` FOREIGN KEY (`driver_id`) REFERENCES `drivers` (`driver_id`) ON DELETE CASCADE,
  ADD CONSTRAINT `session_results_ibfk_2` FOREIGN KEY (`stage_id`) REFERENCES `stages` (`stage_id`) ON DELETE CASCADE;

--
-- Ограничения внешнего ключа таблицы `stages`
--
ALTER TABLE `stages`
  ADD CONSTRAINT `stages_ibfk_1` FOREIGN KEY (`track_id`) REFERENCES `tracks` (`track_id`) ON DELETE CASCADE;

--
-- Ограничения внешнего ключа таблицы `technical_components`
--
ALTER TABLE `technical_components`
  ADD CONSTRAINT `technical_components_ibfk_1` FOREIGN KEY (`team_id`) REFERENCES `teams` (`team_id`) ON DELETE CASCADE;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

--пилоты, их команды и номера, сортируем по номеру, для директора или менеджера команды
select drivers.driver_full_name, drivers.driver_number, teams.team_name
from drivers, teams
where drivers.team_id = teams.team_id and teams.country = 'Italy'
order by drivers.driver_number asc;

--результаты гонок с именами пилотов и названиями этапов, для менеджера или аналитика
select drivers.driver_full_name, stages.stage_name, session_results.finish_position, session_results.points
from session_results
join drivers on session_results.driver_id = drivers.driver_id
join stages on session_results.stage_id = stages.stage_id;

--общая статистика по очкам в таблице результатов, для директоора
select
    count(*) as total_rows,
    sum(points) as sum_points,
    avg(points) as avg_points,
    max(points) as max_points,
    min(points) as min_points
from session_results;

--сколько очков набрал каждый пилот, оставляем тех, у кого больше 10, для директора или менеджера
select driver_id, sum(points) as total_pts
from session_results
group by driver_id
having sum(points) > 10;

--пилоты, которые участвовали хотя бы в одном этапе из таблицы, для аналитика
select driver_full_name
from drivers
where driver_id in (select driver_id from session_results);

select driver_id, stage_id, points
from session_results
where points >= all (select points from session_results where points is not null);

--помечаем, есть ли очки и финишировал ли пилот, для аналитика или болещиков
select
    driver_id,
    stage_id,
    points,
    case
        when points >= 25 then 'pobeda'
        when points > 0 then 'v ochkah'
        else 'bez ochkov'
    end as result_note
from session_results;

--постоянное представление для частого просмотра результатов, для менеджера или аналитика
create view v_race_results as
select drivers.driver_full_name, teams.team_name, session_results.stage_id, session_results.points
from session_results
join drivers on session_results.driver_id = drivers.driver_id
join teams on drivers.team_id = teams.team_id;

select * from v_race_results;

with top_drivers as (
    select driver_id, sum(points) as pts
    from session_results
    group by driver_id
)
select drivers.driver_full_name, top_drivers.pts
from top_drivers
join drivers on top_drivers.driver_id = drivers.driver_id;

--смотрим план запроса до индекса, администатор БД
explain select * from drivers where team_id = 'TEAM-01';

create index idx_drivers_team on drivers(team_id);

explain select * from drivers where team_id = 'TEAM-01';

--добавляем штраф и потверждаем, для судьи
start transaction;

insert into penalties values ('PILOT-016', 'GP-2026-12', 'Track limits', '5 sec');

commit;

--подготавливаем запрос по коду пилота, для Админимстатора
prepare stmt_pilot from 'select * from session_results where driver_id = ?';

set @p_id = 'PILOT-016';
execute stmt_pilot using @p_id;

deallocate prepare stmt_pilot;
