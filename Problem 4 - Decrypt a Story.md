# Problem 4 - Decrypt a Story

def decrypt_story():
    task_text=get_story_string()
    task_message=CiphertextMessage(task_text)
    ans=task_message.decrypt_message()
    return ans
