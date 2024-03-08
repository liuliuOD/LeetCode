![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1125. [Smallest Sufficient Team](https://leetcode.com/problems/smallest-sufficient-team)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 23/38) :
```python
class Solution:
    def smallestSufficientTeam(self, req_skills: List[str], people: List[List[str]]) -> List[int]:
        req_skills = set(req_skills)
        people = sorted(enumerate(people), key=lambda item: len(item[1]))
        queue = deque([([], req_skills)])
        while queue:
            need_people, need_skill = queue.popleft()

            if len(need_skill) == 0:
                return need_people
            for index_person, skill_person in reversed(people):
                if len(need_skill.difference(skill_person)) == len(need_skill):
                    continue
                
                queue.append((need_people + [index_person], need_skill.difference(skill_person)))
```

Method 2 (ERROR: "Time Limit Exceeded", 36/38) :
```python
class Solution:
    def smallestSufficientTeam(self, req_skills: List[str], people: List[List[str]]) -> List[int]:
        req_skills = set(req_skills)
        people = sorted(enumerate(people), key=lambda item: len(item[1]))
        queue = deque([([], req_skills)])
        visited_group = set()
        while queue:
            need_people, need_skill = queue.popleft()

            if len(need_skill) == 0:
                return need_people
            for index_person, skill_person in reversed(people):
                if len(need_skill.difference(skill_person)) == len(need_skill):
                    continue
                
                next_people = sorted(need_people + [index_person])
                next_hash = tuple(next_people)
                if next_hash in visited_group:
                    continue
                visited_group.add(next_hash)

                queue.append((next_people, need_skill.difference(skill_person)))
```

Method 3 (BFS + Bitmask) :
```python
class Solution:
    def smallestSufficientTeam(self, req_skills: List[str], people: List[List[str]]) -> List[int]:
        n = len(req_skills)
        req_skills = {skill_name: skill_ordinal for skill_ordinal, skill_name in enumerate(req_skills)}
        # transfer skills of people to bitmask to prevent sort when check is been visited
        for index_person, person in enumerate(people):
            skills = 0
            for skill in person:
                skills += (1<<req_skills[skill])
            people[index_person] = skills

        queue = deque([([], 2**n - 1)])
        visited_skills_group = set()
        while queue:
            need_people, need_skill = queue.popleft()

            if need_skill == 0:
                return need_people

            for index_next, skills in enumerate(people):
                # remove we need skills that current user has
                need_skill_next = need_skill ^ (need_skill & skills)
                if need_skill_next in visited_skills_group:
                    continue
                visited_skills_group.add(need_skill_next)

                queue.append((need_people + [index_next], need_skill_next))
```
