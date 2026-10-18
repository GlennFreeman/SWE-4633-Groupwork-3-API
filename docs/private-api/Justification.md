---
title: Why These Are Private
nav_order: 7
parent: Private API
---

# Why These Services Are Private

The public API is what a student client needs: log in, see assigned scenarios, take them, see your own scores. Everything in the private API is a service only the faculty CMS should call. The reasons:

## 1. Users: account and role control
The Users endpoints create accounts and set roles. If anyone could call them, a person could make themselves an admin, or reset another user's password. Account administration is a staff job, so it is admin only.

## 2. Scenarios, prompts and answers: they hold the answer key
The scenario endpoints return `points` and `next_prompt_id` for every answer. That is the answer key and the branching map. The public API deliberately leaves these out. If a student could call the private endpoints they could read the best answers before taking the scenario, which ruins the assessment. Editing endpoints are also private so nobody outside the faculty can change what is being graded.

## 3. Classes and courses: they decide who gets what
These endpoints control which students are in which class and which courses a class sees. Letting a client call them would let students enroll themselves in classes, skip assignments or remove classmates. In the public API, assignment is only a result the student sees, never something they set.

## 4. Results: other students' grades are private
The Results endpoints return every student's scores and answers. A student may only see their own attempts, which the public API already provides. Exposing everyone's scores would leak grades between students.

## 5. Different users and different change rate
Only the CMS needs these services, so no outside developer depends on them. The team can change or rename them freely. The public API is a promise to other developers, so it should stay stable and small.

## How "private" is enforced
Hiding the documentation is not security. The private endpoints are protected by the access token's role: the server rejects any token whose role is not `instructor` or `admin` (and only `admin` for Users) with `403`.