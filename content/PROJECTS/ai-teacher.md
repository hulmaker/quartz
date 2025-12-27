---
tags:
  - on/ai
link: https://github.com/Flipajs/ai-teacher
---
- [ ] use GH wiki to write a documentation
- [ ] use GH project for project management
- [ ] Log in to the Oracle account (waiting for mail e@h or he@g)
- [ ] Setup a free [Oracle VM](https://blogs.oracle.com/developers/post/how-to-set-up-and-run-a-really-powerful-free-minecraft-server-in-the-cloud) on [Oracle Free Tier](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm). Checkout [Free product directory](https://www.oracle.com/cloud/free/)
- [ ] landing page [builder list](https://zapier.com/blog/best-landing-page-builders/)
- [ ] pitch deck

## Pitch Deck
Illustrations: [open peeps](https://www.openpeeps.com/), [drawkit](https://www.drawkit.com/search-results?search=stress), [humaaans](https://www.humaaans.com/), [undraw](https://undraw.co/), [blush](https://blush.design/)
[slides](https://slidesgo.com/pitch-deck), [opt1](https://slidesgo.com/theme/problem-based-learning#search-learning&position-17&results-10336&rs=search&rs=search), [opt2](https://slidesgo.com/theme/dealing-with-stress#search-Illustration&position-42&results-11116)

#### Why, How, What
Why:
• Too many things to remember
• Not enough time
• Various sources: videos, podcasts, blogs
• Unstructured information
How:
• turn unstructured information into structured learning materials
• Connect the dots between bits of knowledge with various games
• science-based - spaced repetition, active recall games, habits
What:
• Create structured learning resources from various sources (YT, ...)
• Build protocol for science-based learning
• Build a habit to finally learn what you really want!

# Deploy, hosting, cicd
api key je v lastpass secure note pod ai-teacher
oracle free tier - erik@hulmak.cz
ARM, 4 core OCPU, 24 GB memory, 4 Gbps network bandwidth

[out of capacity](https://www.reddit.com/r/oraclecloud/comments/zf0tje/out_of_capacity_for_shape_vmstandarda1flex/)
```js
let adIndex = 0; // Start with the first AD
setInterval(function() {
    let ads = document.querySelectorAll("input[name='availabilityDomain']"); // Select all AD radio inputs
    if (ads.length > adIndex) {
        ads[adIndex].click(); // Select the next AD
        console.log("Switched to AD " + (adIndex + 1));
        let createButton = document.querySelector(".oui-savant__Panel--Footer .oui-button.oui-button-primary");
        if (createButton && createButton.textContent == "Create") {
            createButton.click();
            console.log("Clicked Create on AD " + (adIndex + 1));
        } else {
            console.log("No Create button found on AD " + (adIndex + 1));
        }
        adIndex = (adIndex + 1) % ads.length; // Move to the next AD, loop back to the first AD after the last one
    } else {
        console.log("No ADs found");
    }
}, 30000); // Run every 30 seconds
```

## db
```sqlite
sqlite3
.open "ai_teacher/instance/ai_teacher.db"
```

koukni na tohle: https://www.youtube.com/watch?v=f5AlQE0i5m0
deploy: https://flask.palletsprojects.com/en/stable/tutorial/deploy/#build-and-install


# Body 
- ssh uz by ses mel byt schopny pripojit
- wiki
- project
- hosting - oracle, vs google
- jak to udelat - docker?
- landing page - debata o tom jak ma vypadat ten produkt


This instruction: https://github.com/google-github-actions/auth?tab=readme-ov-file#direct-wif

workload identity pool id:
projects/1000668196687/locations/global/workloadIdentityPools/github


GITHUB_ORG=AI-Teacher-Sandbox
GITHUB_REPO=ai-teacher

  Workload Identity Provider resource name:
  projects/1000668196687/locations/global/workloadIdentityPools/github/providers/ai-teacher


iam.serviceAccounts.getAccessToken
secret manager secret accessor
compute login

## Installed on instace
git

### Deploy manually
export IMAGE_NAME="ai-teacher-48195c81e31196799786816dc55238b62cc5990b:48195c81e31196799786816dc55238b62cc5990b"
docker load < "/tmp/${IMAGE_NAME}.tar"

ai-teacher-e09433ddaef70499ad043eab4d492506da032379.tar

gcloud compute ssh instance-20241114-165719 --command \ "export API_KEY=$API_KEY; cd /tmp && ./update_image_version.sh --image-name ai-teacher-e09433ddaef70499ad043eab4d492506da032379:e09433ddaef70499ad043eab4d492506da032379


docker run --rm -e API_KEY=$API_KEY ai-teacher-48195c81e31196799786816dc55238b62cc5990b:48195c81e31196799786816dc55238b62cc5990b python -m pytest --root-dir="ai_teacher"

[[gcloud console cheatsheet]]