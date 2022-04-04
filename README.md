# Bonjour et bienvenue dans notre Auto-école !

**Cette application va gerer la prise de rendez-vous pour les leçons de conduite de nos chers étudiants**


## Les informations Business:
- Horaires d'ouvertures 9h-14h 15h-19h du Lundi au vendredi.
- Les horaires weekend sont: 9h-12 15h-17h 
- Nom des professeurs disponible: Mehdi et Julie (Pour plus de simplicité on considère qu'ils sont tous les deux disponibles tous les jours d'ouverture; oui ils sont exploités).
- La duree maximum d'une session est une heure.
- Un seul éleve maximum par session.


## Les fonctionalités:

**Planning sur J à J+7 (si on est mardi, on veut le planning jusqu'à mardi prochain)**

```
calendar = Calendar.new
calendar.current_week

=>	[
		{
			day: '2022-04-04',
			available_sessions: [...],
			booked_sessions: [...]
		},
		{
			day: '2022-04-05',
			available_sessions: [...],
			booked_sessions: [...]
		},
		...
	]
```

**Réservation de Leçon de conduite**  

On va considérer que les élèves savent faire des demandes en JSON (comme le ferai une App Front) et que notre App sait interpréter ces données et répondre de façon adaptée.  
Si le teacher est `nil`, un teacher disponible sera sélectionné par default.  


```
calendar = Calendar.new

request = {
	date: '2022-04-04',
	email: 'fatima@me.com'
	time: '14',
	teacher: 'julie'
}

calendar.book(request)

=> 	{
		status: 200,
		message: 'Session booked'
	}

=> 	{
		status: 400,
		message: 'Invalid parameters'
	}
```

**Récupération des leçons pour chaque élève**

```
calendar = Calendar.new

calendar.my_bookings('guy@gmail.com')

=> 	{
		status: 200,
		list: [...]
	}

=> 	{
		status: 400,
		message: 'Email not found'
	}
```

## TIPS

**Les objets conseillés : (liste non exhaustive)**

- Student
- Teacher
- Lesson
- Calendar

L'architecture pourrai par exemple ressembler à:  

```
calendar-challenge  
  |-- lib  
    |-- student.rb  
    |-- teacher.rb  
    |-- calendar.rb
    |-- lesson.rb  
  |-- bin  
    |-- print_week_calendar.rb  
  |-- spec  
    |-- lib
      |-- student_spec.rb  
      |-- teacher_spec.rb  
      |-- calendar_spec.rb
      |-- lesson_spec.rb  
    |-- spec_helper.rb  
  |-- .git  
  |-- Gemfile
```

Mais n'hésitez pas à créer votre propre architecture si vous le souhaitez.  

N'oubliez pas que nous aimons **beaucoup** les tests, que ce soit pour les cas standard ou les 'edge cases'.  

**Bonne chance :)**
