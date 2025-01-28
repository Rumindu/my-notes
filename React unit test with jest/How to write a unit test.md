# How to Write a unit test?
- This is the `Table` component, we are planing to do unit tests.
``` tsx
"use client";
import {
  TableLayout,
  TableCell,
  TableRow,
} from "@/app/recruiter/jobs/[id]/find-candidates-search-result/components/applications-table";
import { TableActionUpdateStatus } from "@/app/recruiter/jobs/[id]/find-candidates-search-result/components/table-action-update-status";
import { Checkbox } from "@/components/ui/checkbox";
import { cn } from "@/lib/utils";
import { useSelection } from "@/app/recruiter/jobs/[id]/find-candidates-search-result/components/selection-context";

const headings = [
  "",
  "#",
  "Name",
  "Current Designation",
  "Proposed Designation",
  "Status",
  "Matching Score",
  "Actions",
];
export type Applicant = {
  id: string;
  name: string;
  currentDesignation: string;
  proposedDesignation: string;
  matchingScore: number;
  status: string;
  action: string;
};
type FindCandidatesSearchResultTableProps = {
  applicants: Array<Applicant>;
};

export default function Table({
  applicants,
}: FindCandidatesSearchResultTableProps) {
  const { selectedIds, toggleSelection } = useSelection();

  const ActionDisplay = ({ action }: { action: string }) => {
    return (
      <div className="flex h-10 w-full min-w-36 items-center justify-between rounded-md border border-input bg-background px-3 py-2 text-sm text-muted-foreground">
        {action}
      </div>
    );
  };
  if (applicants.length === 0) {
    return (
      <TableLayout headings={headings}>
        <TableRow>
          <TableCell colSpan={10} className="text-center">
            No data found
          </TableCell>
        </TableRow>
      </TableLayout>
    );
  }

  return (
    <TableLayout headings={headings}>
      {applicants.map((application) => (
        <TableRow
          key={application.id}
          className={cn("bg-neutral-100", application.action && "bg-green-300")}
        >
          <TableCell>
            <Checkbox
              checked={
                application.action ? true : selectedIds.includes(application.id)
              }
              disabled={!!application.action}
              onCheckedChange={() => toggleSelection(application.id)}
            />
          </TableCell>
          <TableCell>{application.id}</TableCell>
          <TableCell>{application.name}</TableCell>
          <TableCell>{application.currentDesignation}</TableCell>
          <TableCell>{application.proposedDesignation}</TableCell>
          <TableCell>{application.status}</TableCell>
          <TableCell>{`${application.matchingScore}/10`}</TableCell>
          <TableCell>
            {application.action ? (
              <ActionDisplay action={application.action} />
            ) : (
              <TableActionUpdateStatus
                data={{ applicationId: application.id.toString() }}
              />
            )}
          </TableCell>
        </TableRow>
      ))}
    </TableLayout>
  );
}
```
[source code](https://github.com/Rumindu/interview-process-comments/blob/bb0afdda62e41c4ce580f374985f98891ee5779d/app/recruiter/jobs/%5Bid%5D/find-candidates-search-result/components/table.tsx)

## Unit Testing Plan for Table Component
### 1. Analysis of Dependencies to Mock
- `useSelection` hook (external context)
- `TableLayout`, `TableCell`, `TableRow` components
- `TableActionUpdateStatus` component
- `Checkbox` component

### 2. Test Structure Using 3A Pattern 
- Arrange: Setup test data and mocks
- Act: Render component/trigger actions
- Assert: Verify expected outcomes

### 3. Required Mocks **Setup**
``` tsx 
jest.mock(
  // First param: Module path to mock
  "@/app/recruiter/jobs/[id]/find-candidates-search-result/components/selection-context",
  // Second param: Factory function returning mock implementation
  () => ({
    useSelection: jest.fn(), // Creates a mock function for useSelection hook
  })
);

jest.mock('../applications-table', () => ({
  TableLayout: ({ children }: { children: React.ReactNode }) => <div data-testid="table-layout">{children}</div>,
  TableCell: ({ children }: { children: React.ReactNode }) => <div data-testid="table-cell">{children}</div>,
  TableRow: ({ children }: { children: React.ReactNode }) => <div data-testid="table-row">{children}</div>
}))

jest.mock('../table-action-update-status', () => ({
  TableActionUpdateStatus: () => <div data-testid="action-update-status">Update Status</div>
}))

jest.mock('@/components/ui/checkbox', () => ({
  Checkbox: ({ checked, onCheckedChange }: any) => (
    <input 
      type="checkbox" 
      checked={checked} 
      onChange={onCheckedChange} 
      data-testid="checkbox"
    />
  )
}))
```

### 4. Test Implementation
``` tsx 
describe("Table Component", () => {
  // Mock data setup
  const mockToggleSelection = jest.fn();
  const mockApplicants = [
    {
      id: "1",
      name: "John Doe",
      currentDesignation: "Developer",
      proposedDesignation: "Senior Developer",
      matchingScore: 8,
      status: "Active",
      action: "",
    },
  ];

  beforeEach(() => {
    // Reset mocks before each test
    jest.clearAllMocks();
    // Setup default mock implementation
    (useSelection as jest.Mock).mockReturnValue({
      selectedIds: [],
      toggleSelection: mockToggleSelection,
    });
  });

  describe("Empty State", () => {
    test("should show no data message when applicants array is empty", () => {
      // Arrange
      const emptyApplicants: Applicant[] = [];

      // Act
      render(<Table applicants={emptyApplicants} />);

      // Assert
      expect(screen.getByText("No data found")).toBeInTheDocument();
    });
  });

  describe("Populated State", () => {
    test("should render applicant row with correct data", () => {
      // Arrange & Act
      render(<Table applicants={mockApplicants} />);

      // Assert
      expect(screen.getByText("John Doe")).toBeInTheDocument();
      expect(screen.getByText("8/10")).toBeInTheDocument();
    });

    test("should handle checkbox selection", async () => {
      // Arrange
      render(<Table applicants={mockApplicants} />);

      // Act
      const checkbox = screen.getByTestId("checkbox");
      await userEvent.click(checkbox);

      // Assert
      expect(mockToggleSelection).toHaveBeenCalledWith("1");
    });
  });

  describe("Action Display", () => {
    test("should show ActionDisplay when action exists", () => {
      // Arrange
      const applicantWithAction = [
        {
          ...mockApplicants[0],
          action: "Completed",
        },
      ];

      // Act
      render(<Table applicants={applicantWithAction} />);

      // Assert
      expect(screen.getByText("Completed")).toBeInTheDocument();
    });
  });
});
```
- [Point 3 &4 source code](https://github.com/Rumindu/interview-process-comments/blob/bb0afdda62e41c4ce580f374985f98891ee5779d/__tests__/app/recruiter/jobs/%5Bid%5D/find-candidates-search-result/components/table.test.tsx)
### 5. Explanation of Test Utilities

#### beforeEach
- Used to reset mocks and setup common test conditions
- Ensures each test starts with a clean slate
- Reduces code duplication

#### jest.clearAllMocks()
- Resets mock function call history
- Prevents test interference

#### jest.mock()
- Replaces real implementations with test doubles
- Isolates component for true unit testing
- Simplifies complex dependencies

#### describe blocks
- Groups related tests
- Provides better test organization and readability
- Allows shared setup with nested beforeEach

#### userEvent vs fireEvent
- userEvent simulates real user interactions
- More reliable for testing user interactions
- Handles events in a more realistic way

This structure follows unit testing best practices by:
1. Isolating the component
2. Testing one thing at a time
3. Following the 3A pattern
4. Maintaining clear test organization
5. Using appropriate mocks and stubs