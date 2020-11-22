# ASYNC/AWAIT

instead of .then

ex - >
```javascript
const db = require('./models');

(async () => {
  const [toy, created] = await db.toy.findOrCreate({
    where: { type: 'ball2', color: 'green' },
  });

  const allpets = await toy.getPets();

  if (allpets.length > 0) {
    console.log('all these pets have this toy');
  } else {
    const [pet, created] = await db.pet.findOrCreate({
      where: { name: 'aslkgj', species: 'animal' },
    });

    await toy.addPet(pet); // dont need to assign because we're not using the info thats returned
    console.log('done');
  }
})();
```