# Query
- Selezionare tutti gli studenti nati nel 1990 *(160)*
    - SELECT *  
    FROM `students`  
    WHERE YEAR(`date_of_birth`) = 1990; 

- Selezionare tutti i corsi che valgono più di 10 crediti *(479)*
    - SELECT *  
    FROM `courses`  
    WHERE `cfu` > 10;

- Selezionare tutti gli studenti che hanno più di 30 anni
    - SELECT *   
    FROM `students`   
    WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea *(286)*
    - SELECT *  
    FROM `courses`
    WHERE `year` = 1  
    AND  
    `period` = 'I semestre';

- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 *(21)*
    - SELECT *  
    FROM `exams`  
    WHERE HOUR(`hour`) >= 14  
    AND  
    `date` = '2020-06-20';

- Selezionare tutti i corsi di laurea magistrale *(38)*
    - SELECT *  
    FROM `degrees`  
    WHERE `level` = 'magistrale';

- Da quanti dipartimenti è composta l'università? *(12)*
    - SELECT COUNT(*) AS `numero_dipartimenti`  
    FROM `departments`;

- Quanti sono gli insegnanti che non hanno un numero di telefono? *(50)*
    - SELECT *  
    FROM `teachers`  
    WHERE `phone` IS NULL;

## BONUS
- Contare quanti iscritti ci sono stati ogni anno
    - SELECT COUNT(*) AS `numero_iscritti`,  YEAR(`enrolment_date`) AS `anno_accademico`  
    FROM `students`  
    GROUP BY `anno_accademico`  
    ORDER BY `anno_accademico`;

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio
    - SELECT COUNT(*) AS `numero_insegnanti`, `office_address` AS `indirizzo_ufficio`  
    FROM `teachers`  
    GROUP BY `indirizzo_ufficio`  
    HAVING `numero_insegnanti` > 1  
    ORDER BY `indirizzo_ufficio`;

- Calcolare la media dei voti di ogni appello d'esame
    - SELECT AVG(`vote`) AS `media_voti`, `exam_id` AS `appello_esame`  
    FROM `exam_student`  
    GROUP BY `appello_esame`  
    ORDER BY `appello_esame`;

- Contare quanti corsi di laurea ci sono per ogni dipartimento
    - SELECT COUNT(*) AS `corsi_di_laurea`, `department_id` AS `dipartimento`  
    FROM `degrees`  
    GROUP BY `dipartimento`;  