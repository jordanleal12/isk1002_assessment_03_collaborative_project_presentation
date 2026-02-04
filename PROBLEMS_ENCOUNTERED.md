# IDENTIFIES & EXPLAINS problems and solutions during the programming of a project

<!--
- Identifies & explains AT LEAST THREE problems encountered during a relevant programming project (_This constitutes three total, so one per team member_)
  - Explains a solution for EACH of those problems.
- At least ONE of these problems must be specific to each team member
  -->

## Jordan

### Jordan's Problem

- During the API development, we built route controllers that performed CRUD database operations and sent back formatted HTTP responses. The problem was, we coded these responses before planning a standardized response structure. We didn't understand exactly what response structure we should be using and why, or how it would effect building the front end.

- For example, here is a response I wrote for returning an array of users:

```js
return res.status(200).json({
  success: true,
  data: { users },
});
```

- Here is one I wrote for returning users friendships:

```js
return res.status(200).json({
  success: true,
  friendships,
});
```

- And here is a response Joss wrote for returning movies that matched search parameters:

```js
// If only one movie is found:
if (movies.length === 1) {
  return response.status(200).json({
    success: true,
    message: "Movie found",
    movie: movies[0],
  });
}

// If movie length is over 1 (same title, different movies):
return response.status(200).json({
  success: true,
  message: `Found ${movies.length} movies with title "${title}"`,
  movies,
});
```

- If you look closely you'll notice some inconsistencies. I was returning the users array under a 'data' key, but friendships under a key of its own name.

- Joss was attaching a message object, and returning a single movie object, or an array of movies in the same route depending on the amount.

- When we became aware of these mistakes, we had to waste time reformatting all the existing controllers and tests to standardize the response format.

- Some of the controllers were missed during this reformatting, leading to puzzling errors during front end development

- For example, there were times when array methods were causing errors as the response would have either an object or an array attached depending on the quantity.

### Jordan's Solution

- If we were to do this project again, I would implement a structured planning approach to address this issue.

- Firstly, we would identify what data the frontend application needed in the responses.

- Secondly, we would identify what would constitute success for a response. For example, we had some initial confusion over whether searching for something in the database should return an unsuccessful response, or a success response with an empty array or object

- Thirdly, we would identify what data structure to use. Would requested data use a 'data' key? Should all requested data be in an array, or only return data in arrays when there is more than one possible data object to return? This should be decided through the lens of the front end application, looking at which options would be easiest and most consistent to work with

- Lastly, identify the remaining response structure. For example, should we use an array for our error messages? should it be attached but empty on success? Should a message always be attached for success? What structure will be the easiest and most consistent to work with for our frontend? Are there packages we can use to ensure a consistent response is sent, eliminating human error?

---

## Joss

### Joss' Problem

### Joss' Solution

---

## Nhi

### Nhi's Problem

### Nhi's Solution
