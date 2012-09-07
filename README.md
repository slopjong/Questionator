Questionator
============

Questionator? What is this?


If you were writing an exam simulator used to test the knowledge base of something the exam takers have studied, you need a certain format for your questionary that the program can read in.

Preparation
-------------------

An exam writer is asked to create a hierarchical directory structure of questions and answers as shown below.

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

Biology here stands for the certification name, Bio-1 and Bio-2 are the certification levels with 101, 102 etc. standing for the single exams. The exams are further devided into chapters where the actual questions and answers reside in.

The content of the questions and answers files follow a pattern. Questions are enumerated with digits while answer options are alphabetically enumerated.

```
1. What of the human body is not an organ?
A. Lung
B. Heart
C. Leg
D. Stomach
2. Which of the following is a valve of the human heart?
A. Tricuspid Valve
B. Tricupsid Valve
C. Dricupsit Valve
D. Cupsidrit Valve

```

The questions and answers can wrap multiple lines, there's no restriction such as an option per line. In the above example you see two questions with its answer options.

<!---
In every directory level you can have a title file which keep a more verbous version of the title. The directory names e.g. Biology, Bio-1 and 102 are used unmodified to
-->

Generating the questionary
--------------------------------------------

After the directory structure is created you run the build-catalog script which then takes this directory structure and brings everything together in a JSON file. This generated file can be used in any web and desktop application that is able to interpret JSON.

Why is the above directory structure not used directly? It's a lot more comfortable to share one single file with the whole questionary instead of a bunch of files. Creating an archive would be an option but then the users and applications are required to use an unarchiver.

To run the build-catalog script you need to provide it

* php
* json_reformat (contained in the yajl library)
* sponge (contained in the moreutils toolkit)

Here is what the catalog generator finally produces:

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
        "3": {
            "question": "Which of the following is not part of the structure of a typical neuron?",
            "options": [
                "Dendrite",
                "Nucleus",
                "Axon",
                "Samo"
            ],
            "correct": [
                3
            ],
            "explanation": "Soma is a part of the structure of a neuron but samo is fictous. Thus options A, B and C are correct but not D.",
            "category": "102.03"
        },
        "4": {
            "question": "What statement is wrong?",
            "options": [
                "Neurones occur only in the nervous system, but they are not the unique type of cells in it: there are, also, the glial cells, which assist the neurones in several tasks.",
                "The demyelination of myelinated axons is characteristic of some serious diseases such as multiple sclerosis.",
                "The function of neurones is transmitting an electric current called nerve impulse along circuits that connect the sensory information collected by the receptors with the responses performed by the effectors.",
                "None is wrong."
            ],
            "correct": [
                3
            ],
            "explanation": "The listed facts about neurones are all correct.",
            "category": "102.03"
        },
        "5": {
            "question": "Which of the following is a non-human sense?",
            "options": [
                "Sight",
                "Taste",
                "Kinestetic sense",
                "Pain",
                "Time",
                "Above listed senses are all human."
            ],
            "correct": [
                5
            ],
            "explanation": "All listed senses are present in a human body. Sight or vision is the capability of the eye(s) to focus and detect images of visible light on photoreceptors in the retina of each eye that generates electrical nerve impulses for varying colors, hues, and brightness. Taste is one of the traditional five senses. It refers to the capability to detect the taste of substances such as food, certain minerals, and poisons, etc. Proprioception, the kinesthetic sense, provides the parietal cortex of the brain with information on the relative positions of the parts of the body. Nociception (physiological pain) signals nerve-damage or damage to tissue. Chronoception refers to how the passage of time is perceived and experienced. Although the sense of time is not associated with a specific sensory system the work of psychologists and neuroscientists indicates that human brains do have a system governing the perception of time.",
            "category": "101.02"
        },
        "6": {
            "question": "What is not a functional sense of the dolphin species?",
            "options": [
                "Echolocation",
                "Electroception",
                "Magnetoception",
                "Dolphins have none of the above"
            ],
            "correct": [
                2
            ],
            "explanation": "In common dolphins (Delphinus delphis) magnetite has been found but its biological use is still not proven. The vibrissal crypts of the Guiana dolphin (Sotalia guianensis) were shown to be capable of electroreception sufficient to detect small fish, as low as 4.8 Î¼V/cm. The dolphin's head contains the melon, a round organ used for echolocation. Dolphin teeth are believed to function as antennae to receive incoming sound and to pinpoint the exact location of an object. Beyond locating an object, echolocation also provides the animal with an idea on the object's shape and size, though how exactly this works is not yet understood.",
            "category": "101.02"
        },
        "7": {
            "question": "What of the human body is not an organ?",
            "options": [
                "Lung",
                "Heart",
                "Leg",
                "Stomach"
            ],
            "correct": [
                2
            ],
            "explanation": "A leg is a locomotive structure and doesn't cooperate with any organ system. A, B and D are all providing a certain function and with functionally related organs forming an organ system.",
            "category": "101.01"
        },
        "8": {
            "question": "Which of the following is a valve of the human heart?",
            "options": [
                "Tricuspid Valve",
                "Tricupsid Valve",
                "Dricupsit Valve",
                "Cupsidrit Valve"
            ],
            "correct": [
                0
            ],
            "explanation": "The first option is correct because B, C and D are fictious.",
            "category": "101.01"
        }
    }
}
```