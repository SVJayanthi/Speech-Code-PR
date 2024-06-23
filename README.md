# Speech-Code-PR

## Overview
End-to-end AI pipeline that converts an audio file (like a meeting recording) using **Automatic Speech Recognition** to a **Code Spec**, then performs **Code Search** to do **Code Generation**, and generates a pull request to Github.

### Example Audio File
<audio controls>
  <source src="DesignDiscussion.wav" type="audio/wav">
  Audio file `DesignDiscussion.wav`
</audio>

**Produced transcription**

    Hi all, thanks for joining. Today we're going to discuss the feature revamp for the multimodal RAG application to improve user experience. First on our list is adding a chat functionality to the application so that users can maintain chat history and ask questions over some of the previous interactions they've had with the application. In order to work successfully we need to ensure there is a chat reset, a chat delete, and a chat modal that keeps track of all the different chats our user is having with their application in context.

**Built Code Spec**
### Code Spec for Multimodal RAG Application Feature Revamp

**Objective Statement:**
- The main objective of this feature is to provide an enhanced user experience by adding chat functionality to the multimodal RAG application.

**Requirements:**
- **Functional:**
  - The system must allow users to maintain chat history.
  - The feature should enable users to ask questions based on their previous interactions.
  - The system must include functionalities for chat reset and chat delete.
- **Non-functional:**
  - N/A (not specified in the transcript).

**Use Case/User Story:**
- As a user, I want to maintain and interact with chat history to ask follow-up questions based on my previous interactions with the application.

**Deliverables:**
- **Design New File:**
  - Design a new chat modal to keep track of all the different chats in context.
- **Modify Existing File:**
  - N/A (not specified in the transcript).
- **Documentation:**
  - Document the new chat functionalities including chat reset and delete in detail.

**Code Change**
```
def chat_management() -> rx.Component:
    """Component for managing chat functionalities."""
    
    return rx.chakra.hstack(
        rx.chakra.button(
            "Reset Chat",
            on_click=State.reset_chat
        ),
        rx.chakra.button(
            "Delete Chat",
            on_click=State.delete_chat
        )
    )

# Add state and page to the app.
app = rx.App(
    theme=rx.theme(
        appearance="dark",
        accent_color="violet",
    ),
)

app.add_page(index)
app.add_page(chat_management, route="manage_chat")
```


## Application Pipeline
1. **Audio File Upload**

The audio from your meeting or discussion is used to both design a Code Spec and to ultimately perform a code change in your repostory.

2. **Automatic Speech Recognition (ASR)**

Once the audio file is uploaded, it is processed using Whisper, a powerful ASR model thats converts the spoken content in the audio file into written text. This transcription includes all the discussions, decisions, and instructions from the meeting, providing a comprehensive textual representation of the meeting's content.

3. **Code Specification Generation**

The transcribed text from the meeting is then used to generate a detailed code specification. This involves parsing the transcript to extract key information such as objectives, functional and non-functional requirements, user stories, and deliverables.

4. **Code Retrieval**

With the code specification in hand, the next step is to retrieve the relevant files from the code repository that will be impacted by the new feature or change. This is done by creating a RAG framework over the codebase & indexing the content of the code along with relevant metadata.

5. **Context Building**

After finding the relevant file, we build context around the file by traversing all imports within the repository and documenting the dependency hierarchy to provide all context required to make a successful code change.

6. **Code Generation**

Using the detailed code specification and the gathered context, an LLM is used to generate the required code changes. This involves modifying existing files or creating new ones to implement the specified features or fixes.

7. **Pull Request Creation**

Finally, automate the process of creating a draft pull request (PR) on GitHub to integrate the generated code changes. This step ensures that the changes are reviewed and merged following the standard development workflow.


## Example Use Cases
1. **Sprint Planning Meetings**

During a sprint planning meeting, team members discuss the features they will work on for the upcoming sprint. By recording the meeting and using this AI pipeline, the audio can be converted into code specifications for each discussed feature. These specifications are then used to generate draft PRs for all team members, jumpstarting their development work. This ensures that everyone starts with a clear and consistent understanding of the tasks and reduces the time spent on initial setup and documentation.

2. **Product Design Requirements**

In design discussion sessions, various architectural and design decisions are made. Recording these sessions and running the pipeline can create detailed code specifications reflecting the agreed-upon designs. This helps in maintaining consistency across the implementation and ensures that all design considerations are documented and followed. The generated PRs can then be reviewed and refined, ensuring alignment with the discussed design.

3. **Client Discussions**

Client meetings where requirements for new features or changes are discussed can be recorded and processed using the pipeline. This ensures that the client’s requirements are accurately transcribed and translated into code specifications. Draft PRs can then be generated based on these specifications, allowing for quick implementation and review of client-requested features.

4. **Bug Triaging**

In bug triage meetings, teams prioritize and assign bugs to be fixed. By recording these meetings, the pipeline can transcribe the discussions and generate code specifications for each bug fix. This can streamline the process of creating PRs for bug fixes, ensuring that all relevant information from the meeting is included in the implementation plan.

*The possibilities are endless!*

## Dependencies
To get started, ensure you have the following dependencies installed per the `requirements.txt` file:
- librosa
- torch
- transformers
- openai
- qdrant-client
- pygithub


### Authors
Sravan, Vedant, Suvansh, Alex, Nithin, Utsav, Aadarsh

*Bronze in 2024 C3 AI Hackathon* 