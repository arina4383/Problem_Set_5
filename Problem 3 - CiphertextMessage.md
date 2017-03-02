# Problem 3 - CiphertextMessage

class CiphertextMessage(Message):
    def __init__(self, text):
        '''
        Initializes a CiphertextMessage object
                
        text (string): the message's text

        a CiphertextMessage object has two attributes:
            self.message_text (string, determined by input text)
            self.valid_words (list, determined using helper function load_words)
        '''
        self.message_text = text
        self.valid_words = load_words(WORDLIST_FILENAME)

    def decrypt_message(self):
        '''
        Decrypt self.message_text by trying every possible shift value
        and find the "best" one. We will define "best" as the shift that
        creates the maximum number of real words when we use apply_shift(shift)
        on the message text. If s is the original shift value used to encrypt
        the message, then we would expect 26 - s to be the best shift value 
        for decrypting it.

        Note: if multiple shifts are  equally good such that they all create 
        the maximum number of you may choose any of those shifts (and their
        corresponding decrypted messages) to return

        Returns: a tuple of the best shift value used to decrypt the message
        and the decrypted message text using that shift value
        '''
        best_value={}
        for shift in range(26):
            final_text=self.apply_shift(26-shift)
            final_text=final_text.split()
            counter=0
            ans=''
            for word in final_text:
                if is_word(self.valid_words,word):
                    counter+=1
                else:
                    counter+=0
            for e in final_text:
                ans+=' '+e    
            ans=ans[1:]
            if shift!=0:
                best_value[counter]=(26-shift,ans)
            else:
                best_value[counter]=(shift,ans)
                
        M=max(best_value.keys())
        return best_value[M]
