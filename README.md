# MA15Y030

Site Ouèbe du cours *Bases de données* MA15Y030 Université Paris Cité UFR de Mathématiques

Pour construire le site, dans cet ordre 

```{.bash}
$ quarto render [--to html]
$ quarto render slides --no-clean
$ quarto render solutions  [--to html] --profile solution --no-clean
$ quarto render exams [--to html] --profile solution --no-clean
```

Pour publier le site 

```{.bash}
$ quarto publish gh-pages --no-render 
```

[https://s-v-b.github.io/MA15Y030/](https://s-v-b.github.io/MA15Y030/)

