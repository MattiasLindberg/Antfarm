# Antfarm Framework Implementation

The reference implementation of Antfarm is built using Python. The language was choose because it is a very popular langues in general
(see [Stackoverflow Developer Survey 2020](https://insights.stackoverflow.com/survey/2020#technology-programming-scripting-and-markup-languages-professional-developers)) 
and that it has many libraries available that are useful for solving problems in physics.

## Dependency Injection
The code uses depedency injection to minimize the need to change the framework code, the user should focus his work on implementing
the orchestration and work code that is unique to his solution. 

The [python-dependency-injection](https://pypi.org/project/python-dependency-injection/) framework is used to support dependency injection.

