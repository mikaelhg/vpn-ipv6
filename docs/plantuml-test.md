# PlantUML test

```plantuml format="png"

Alice -> Bob: Authentication Request

alt successful case

    Bob -> Alice: Authentication Accepted

else some kind of failure

    Bob -> Alice: Authentication Failure
    group My own label
    Alice -> Log : Log attack start
        loop 1000 times
            Alice -> Bob: DNS Attack
        end
    Alice -> Log : Log attack end
    end

else Another type of failure

   Bob -> Alice: Please repeat 2

end

```

/* Oops 2! */

## ChatOps and GitOps links

Chatbot: [https://github.com/hubotio/hubot](https://github.com/hubotio/hubot)

Apps: [https://github.com/probot/probot](https://github.com/probot/probot)
