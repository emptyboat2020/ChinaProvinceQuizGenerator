# ChinaProvinceQuizGenerator
#From Automate the Boring Stuff Ch. 9 - Random Quiz Generator

# randomQuizGenerator.py - Creates quizzes with questions and answers in
# random order, along with the answer key.
import random
# The quiz data. Keys are Provinces and values are their capitals
capitals = {'Anhui': 'Hefei', 'Fujian': 'Fuzhou', 'Gansu': 'Lanzhou', 'Guandong': 'Guangzhou', 'Guangxi': 'Nanning', 'Hainan': 'Haikou', 'Hebei': 'Shijiazhuang', 'Heilongjiang': 'Harbin', 'Henan': 'Zhengzhou', 'Hubei': 'Wuhan', 'Hunan': 'Changsha', 'Inner Mongolia': 'Hohhot', 'Jiangsu': 'Nanjing',
            'Jiangxi': 'Nanchang', 'Jilin': 'Changchun', 'Liaoning': 'Shenyang', 'Ningxia': 'Yinchuan', 'Qinghai': 'Xining', 'Shaanxi': 'Xi/i/an', 'Shandong': 'Jinan', 'Shanxi': 'Taiyuan', 'Sichuan': 'Chengdu', 'Tibet': 'Lhasa', 'Xinjiang': 'Urumuqi', 'Yunnan': 'Kunming', 'Zhejiang': 'Hangzhou'}

provincesItems = list(capitals.keys())

# Generate 35 quiz files.
for quizNum in range(35):
    # Create the quiz and answer key files.
    quizFile = open('capitalsquiz%s.txt' % (quizNum + 1), 'w')
    answerKeyFile = open('capitalsquiz_answers%s.txt' % (quizNum + 1), 'w')

    # Write out the header for the quiz.
    quizFile.write('Name:\n\nDate:\n\nPeriod:\n\n')
    quizFile.write((' ' * 20) + 'Province Capitals Quiz (Form %s)' % (quizNum + 1))
    quizFile.write('\n\n')

    # Shuffle the order of the states.
    provinces = list(capitals.keys())  # get all states in a list
    random.shuffle(provinces)  # randomize the order of the states

    # Loop through all 50 states, making a question for each.
    for questionNum in range(26):

        # Get right and wrong answers.
        correctAnswer = capitals[provinces[questionNum]]
        wrongAnswers = list(capitals.values())  # get a complete list of answers
        del wrongAnswers[wrongAnswers.index(correctAnswer)]  # remove the right answer
        wrongAnswers = random.sample(wrongAnswers, 3)  # pick 3 random ones

        answerOptions = wrongAnswers + [correctAnswer]
        random.shuffle(answerOptions)  # randomize the order of the answers

        # Write the question and answer options to the quiz file.
        quizFile.write('%s. What is the capital of %s?\n' %
                       (questionNum + 1, provinces[questionNum]))
        for i in range(4):
            quizFile.write('    %s. %s\n' % ('ABCD'[i], answerOptions[i]))
        quizFile.write('\n')

        # Write out the answer key to a file.
        answerKeyFile.write('%s. %s\n' %
                            (questionNum + 1, 'ABCD'[answerOptions.index(correctAnswer)]))
    quizFile.close()
    answerKeyFile.close()
