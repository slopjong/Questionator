Questionator
============

Questionator? What is this?

If you were writing an exam simulator used to test the knowledge base of something the exam takers have studied, you need a certain format for your questionary that the program can read in.

There is not only one way to accomplish this task. The way chosen by Questionator is to first create a hierarchical structure of questions and answers which looks like this:

```
Biology
+-- Bio-1
|   +-- 101
|   |   +-- 01
|   |   |   +-- answers.txt
|   |   |   +-- questions.txt
|   |   |   +-- title
|   |   +-- 02
|   |       +-- answers.txt
|   |       +-- questions.txt
|   |       +-- title
|   +-- 102
|   |   +-- 03
|   |       +-- answers.txt
|   |       +-- questions.txt
|   |       +-- title
|   +-- title
+-- Bio-2
    +-- 201
    |   +-- 01
    |       +-- answers.txt
    |       +-- questions.txt
    |       +-- title
    +-- title

```

Questionator takes this directory structure and brings everything together in a JSON file. This generated file can be used in web and desktop applications and makes it easier to share a questionary with others since everything is in one file only. The generated JSON looks like this:

```
{
    "metainf": {
        "name": "Biology",
        "model": 1
    },
    "titles": {
        "level": {
            "Bio-2": {
                "title": "Advanced Level Biology Certification",
                "exam": {
                    "201": {
                        "title": "",
                        "chapter": {
                            "01": "Animals And Plants"
                        }
                    }
                }
            },
            "Bio-1": {
                "title": "Junior Level Biology Certification",
                "exam": {
                    "102": {
                        "title": "",
                        "chapter": {
                            "03": "Nervous System"
                        }
                    },
                    "101": {
                        "title": "",
                        "chapter": {
                            "02": "Sensing",
                            "01": "Exploring Human Organs"
                        }
                    }
                }
            }
        }
    },
    "question_groups": {
        "Bio-2": {
            "201": {
                "01": [
                    1,
                    2
                ]
            }
        },
        "Bio-1": {
            "102": {
                "03": [
                    3,
                    4
                ]
            },
            "101": {
                "02": [
                    5,
                    6
                ],
                "01": [
                    7,
                    8
                ]
            }
        }
    },
    "questions": {
        "1": {
            "question": "What statement about sea stars is incorrect?",
            "options": [
                "No species are simultaneous producing eggs and sperm at the same time.",
                "In some species young individuals are males that change into females as they grow larger.",
                "In some species, when a large female divides, the smaller individuals produced become males. When they grow big enough, they change back into females.",
                "Most species are dioecious, with separate male and female individuals."
            ],
            "correct": [
                0
            ],
            "explanation": "There are some species being able to produce both, eggs and sperm so option A is incorrect.",
            "category": "201.01"
        },
        "2": {
            "question": "What of the following is not classified as a plant?",
            "options": [
                "Algae",
                "Fungus",
                "Venus Flytrap",
                "Pinus sylvestris"
            ],
            "correct": [
                1
            ],
            "explanation": "A fungus is a member of a large group of eukaryotic organisms that includes microorganisms such as yeasts and molds, as well as the more familiar mushrooms. These organisms are classified as a kingdom, Fungi, which is separate from plants, animals, and bacteria.",
            "category": "201.01"
        },
	...
    }
}
```