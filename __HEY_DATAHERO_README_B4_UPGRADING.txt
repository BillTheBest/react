
DATAHERO REACT, v0.13.3 MONKEYPATCH


README BEFORE UPGRADING COPY OF REACT!



We use a monkeypatched version of React.

Long story short, Zendesk widget uses its own packaging of React, and React currently has a bug where multiple
instances of React don't play nicely with each other.

See:
  https://github.com/Datahero/datahero-node/issues/15596
  https://github.com/facebook/react/issues/1939


----------
WHAT THIS MEANS FOR UPGRADING:

1) We had to make a change to our version of React -- we changed the ID_ATTRIBUTE_NAME string to a custom 'data-dh-reactid' to
   isolate our React from the Zendesk React.  

2) There's a weird Backbone router hack.  In main.js, there's a sendToRouter() function that's a global click handler which sends
   all <a> clicks to the backbone handler.  It skips clicks from react elements, as guarded by with a 'data-reactid' check.  This
   has been customized to always abort on 'data-dh-reactid' checks.  This weird hack needs to be adjusted if adding a different
   react namespace.

If upgrading a version React and react#1939 has not yet been resolved, apply the same monkeypatch to the new copy of react.



This file can be deleted once a solution is put in place.

