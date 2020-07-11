Documentation for the BaseState class

This class is a parent-class for all state handlers, it provides:
        - interface to Google Translations API
        - interface to our own phrases/responses
        - automatically translates our strings to the language of the user
        - automatically adds pictures to the chosen intents/conversation steps/questions
        - interface to the database
        - interface to the NLU (Natural Language Understanding unit - https://github.com/HumanbiOS/rasa)
        - automatic requests queueing
        - automatic database updates for the `User` object

Example  
.. function::  
    from . import base_state

    class MyExampleState(base_state.BaseState):
        
        async def entry(self, context, user, db):
            # your entry code goes here
            context['request']['message']['text'] = "Hello World!"
            # you must return status
            return base_state.OK
        
        async def process(self, context, user, db):
            # your process code goes here
            context['request']['message']['text'] = ""
            # i want to move user to other state (referring by name)
            return base_state.GO_TO_STATE("MyNextState")


Available functions:
    
    :py:func:`async def entry(self, context: Context, user: User, db):`
        Function gets executed each time user enrers your state

    :py:func:`async def process(self, context: Context, user: User, db):`
        Function gets executed each time message gets processed by your state (Except when it enters)

    :py:func:`def send(self, to_user: User, context: Context):`
        Function creates task that sends `context['request']` to the `to_user` User after executing your code inside state.

    :py:func:`def create_task(self, func, *args, **kwargs):`
        Function executes async function (with given args and kwargs) immediately after processing state.

    :py:func:`def set_language(self, value: str):`
        Function tells server to translate text to certain language. `value` must be ISO 639-1 Code language code (supported by the Google API)

    :py:func:`def parse_button(self, raw_text: str, truncated=False) -> Button:`
        Function compares input text to all available strings (of user's language) and if finds matching - returns Button object, which has `text` and `key` attributes, where `text` is `raw_text` and `key` is a key of matched string from `strings.json`

    :py:func:`async def download_by_url(self, url, *folders, filename):`
        Function asynchroniously downloads file from given `url` to the given *relative* path (joined folders and filename). The `folders` value will be joined to the default media path. Default media path - PROJ_ROOT/media

    :py:func:`def exists(self, *args):`
        Function checks if file exists under given path

    :py:func:`async def translate(self, text: str, target: str) -> str:`
        Function is wrapper for translation_text from translation module. Simply returns translated `text` for the `target` language. Good usage example if translating text between users.
