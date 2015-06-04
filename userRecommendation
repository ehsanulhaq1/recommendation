import requests
import json
import codecs
from HTMLParser import HTMLParser
from bs4 import BeautifulSoup
import csv
import sys
import urllib2
import csv
import math

LETTER = "P"
userFile = "etl/userFile%s.csv" %LETTER
userLikeFile = "etl/neweltFile%s.csv" %LETTER


# data is stored in csv files, 
# a user u (likes of user u)is given to the code, this code 
# calculates the weights for different categories 
# for user based on other users present in network.
# Other users are stored in csv files. 


def getUserRecommendation(user, letter):
	pageETLFile = "/Users/User/Desktop/fbData/etl/neweltFile%s.csv" %letter
	fileReader = open(pageETLFile, 'rb')
	scoreFile = csv.reader(fileReader)

	userData = user


	userNetwork = user[161:]
	rowCounter = 0

	vScoreArray	= [0]*160

	alpha  = 0.025 * (-1)
	euler = 2.7182 
	decay = pow(euler,alpha)

	intVnet,intUnet = [],[]
	for row in scoreFile:
		if rowCounter == 0:
			rowCounter = 1
			continue

		vNetwork = row[161:]  # user v in network
		
		for x in range (0,5):
			a = int(vNetwork[x])
			b = int(userNetwork[x])
			intVnet.append(a)
			intUnet.append(b)

		relationstrength = 0
				
		x1 = ((intVnet[0] * intUnet[1] + intVnet[1] * intUnet[0]) * .8) + ((intVnet[3] * intUnet[4] + intVnet[4] * intUnet[3]) * .5)


		x2 = 0;
		for it in range(1, 159):
			if it < 41:
				x2 = intVnet[0] * intUnet[0]
			elif it <76:
				x2 = intVnet[1] * intUnet[1]
			elif it < 106:
				x2 = intVnet[2] * intUnet[2]
			elif it < 149:
				x2 = intVnet[3] * intUnet[3]
			else: 
				x2 = intVnet[4] * intUnet[4]

			relationstrength = x1 + x2
			addition = int(row[it]) * (relationstrength * (int(row[it])+int(userData[it])))
			vScoreArray[it] = vScoreArray[it] + (addition * decay)
	
	print "for whole list score is"
	print vScoreArray
	return vScoreArray

stringValue = "value"


# given user is retrieved from a csv file.

testfile = "/Users/User/Desktop/fbData/test/testUser.csv"
testReader = open(testfile, 'rb')
userScoreFile = csv.reader(testReader)


#  get user's data
userArray= []
for row in userScoreFile:
	for x in row:
		userArray.append(x)

print "userArray is %s" %userArray


getUserRecommendation(userArray,LETTER)
