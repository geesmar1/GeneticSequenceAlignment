###################################################
#P1
###################################################
# -*- coding: utf-8 -*-
"""
Created on Mon Oct 19 09:08:04 2020
"""
import os
   
def ParseSeqFile(filepath):
    """
    Parses function file: excluding blankspaces, upper case letters for Nucleotides and sequence ID
    Additional checking if sequences in inputfile are non-DNA sequences.
    
    Parameters
    ----------
    filepath: 
        Takes the filepath (inclusive filename) as input (only .txt formate).
        
    Returns
    -------
    sequence_list: 
        Returns a list containing a tuple for every sequence in the inputfile, containing the sequence ID and the DNA sequence as strings
    """
    
    #importing the .txt file
    try:
         file = open(filepath,"r")
    except:
        return print("malformed input")

    # initializing empy list 
    sequence_list = list()
     
    #Parsing file and inputs
    for line in file:
        if ">" in line[0]: #checking the structure of the file for lines starting with ">"
            elements = list(line.strip("> ").strip("\n").split(" ")) 
            #stripping out ">" and creating list of strings by the delimiter " "
             
            #extracting first element of the line and saving as the species name, writing all letters capital
            species = elements[0].upper()
            # saving all remaining elements as the sequence
            sequence = elements[1:]
            #joning the sequence together to eliminate blankspaces and write all in capital letters
            sequence = "".join(sequence).upper()
           
            #check sequences if it is DNA 
            if  check_if_dna(sequence)== True:
                #concatenate the species and the corresponding sequence in a tuple, appending tuples to the list  
                sequence_list.append((species, sequence))    
                
            # if nn-DNAsequences in input file, printing statement
            else:
                print("non-DNA sequences excluded!")
                
                
    return sequence_list


# external function for check if a sequence in a file is DNA or not
def check_if_dna(Seq):
    #this function checks if a sequence is dna so it can be discriminated between RNA or amino acid sequences.
    sequence = Seq.upper()
    notDNA = "BDEFHIJKLMNOPQRSUVWXYZ"
    
    # iteration through all elements in sequences to check if non-DNA letters are included
    for character in notDNA:
        if character in sequence:
            return False
    return True



A = ParseSeqFile('C:/Users/Marco Gees/OneDrive - ZHAW/ZHAW/Master/V5_1-Programming_Algorithms_and_Data_Structures/Project/Task 1/sequencefile.txt')
# 
print(A)     
      
      
      
      
      
      
      
      
      
