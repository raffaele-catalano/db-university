# Query #2
- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
    - SELECT `students`.`name`, `students`.`surname`, `students`.`id`, `students`.`registration_number`, `degrees`.`name` AS `degree_program`  
    FROM `students`  
    INNER JOIN `degrees`  
    ON `students`.`degree_id` = `degrees`.`id`  
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia'  
    ORDER BY `students`.`surname`; 
- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
    - SELECT `departments`.`name`, `departments`.`address`, `departments`.`website`, `degrees`.`name` AS `degrees_name` , `degrees`.`level`  
    FROM `departments`  
    INNER JOIN `degrees`  
    ON `departments`.`id` = `degrees`.`department_id`  
    WHERE `degrees`.`level` = 'magistrale'  
    AND `departments`.`name` = 'Dipartimento di Neuroscienze'; 
- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    - SELECT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`, `teachers`.`email` , `courses`.`name` AS `course_name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `courses`.`description`  
    FROM `courses`  
    INNER JOIN `course_teacher`  
    ON `courses`.`id` = `course_teacher`.`course_id`  
    INNER JOIN `teachers`  
    ON `course_teacher`.`teacher_id` = `teachers`.`id`  
    WHERE `teachers`.`surname` = 'Amato'  
    AND `teachers`.`id` = 44
    ORDER BY `courses`.`year`;
- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
    - SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `departments`.`name` AS `department_name`  
    FROM `departments`  
    INNER JOIN `degrees`  
    ON `departments`.`id` = `degrees`.`department_id`  
    INNER JOIN `students`  
    ON `degrees`.`id` = `students`.`degree_id`  
    ORDER BY `students`.`surname`;
- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
    - SELECT `degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `degrees`.`email`, `courses`.`name` AS `course_name`, `courses`.`year`, `courses`.`period`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`office_address`, `teachers`.`phone`, `teachers`.`email`  
    FROM `degrees`  
    INNER JOIN `courses`  
    ON `degrees`.`id` = `courses`.`degree_id`  
    INNER JOIN `course_teacher`  
    ON `courses`.`id` = `course_teacher`.`course_id`  
    INNER JOIN `teachers`  
    ON `course_teacher`.`teacher_id` = `teachers`.`id`  
    ORDER BY `degrees`.`name`;
- Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
    - SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`email`, `teachers`.`office_address`, `teachers`.`office_number`  
    FROM `teachers`  
    INNER JOIN `course_teacher`  
    ON `teachers`.`id` = `course_teacher`.`teacher_id`  
    INNER JOIN `courses`  
    ON `course_teacher`.`course_id` = `courses`.`id`  
    INNER JOIN `degrees`  
    ON `courses`.`degree_id` = `degrees`.`id`  
    INNER JOIN `departments`  
    ON `degrees`.`department_id` = `departments`.`id`  
    WHERE `departments`.`name` = 'Dipartimento di Matematica'  
    ORDER BY `teachers`.`surname`;
    ## BONUS
- Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.
    - SELECT